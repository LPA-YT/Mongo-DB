============================================================
                    MONGODB PRACTICE
============================================================
Database: my_dbs
Main Collection: products
============================================================
1. BASIC DATABASE COMMANDS
============================================================

Check current database:
db

Show all databases:
show dbs

Switch to database:
use my_dbs

Show collections:
show collections

============================================================
2. CREATE COLLECTION
============================================================

Create a collection named products:

db.createCollection("products")

Check collections:

show collections


============================================================
3. INSERT 50 PRODUCTS
============================================================

The following JavaScript loop was used to insert 50 products:

for (let i = 1; i <= 50; i++) {

    db.products.insertOne({
        productId: i,
        productName: "Product " + i ,

        category:
            i % 5 === 0 ? "Laptop" :
            i % 5 === 1 ? "Mobile" :
            i % 5 === 2 ? "Headphones" :
            i % 5 === 3 ? "Keyboard" :
                          "Mouse",

        brand:
            i % 3 === 0 ? "Dell" :
            i % 3 === 1 ? "Samsung" :
                          "HP",

        price: 1000 + (i * 500),

        stock: 10 + i,

        rating: 3 + ((i % 3) * 0.5),

        inStock: i % 4 !== 0,

        tags: [
            "electronics",
            i % 2 === 0 ? "featured" : "new"
        ],

        seller: {
            sellerId: 1000 + i,
            sellerName: "Seller " + i
        },

        createdAt: new Date()
    });
}


============================================================
4. VIEW ALL PRODUCTS
============================================================

Display all documents:

db.products.find()

Display one document:

db.products.findOne()


============================================================
5. FIND PRODUCT BY productId
============================================================

Find Product 20:

db.products.find({ productId: 20 })

Find one specific Product 20:

db.products.findOne({ productId: 20 })


============================================================
6. UPDATE PRODUCT 20 - PRICE
============================================================

Original price of Product 20:

11000

Update price to 14999:

db.products.updateOne(
    { productId: 20 },
    { $set: { price: 14999 } }
)

$set is used to set/change the value of a field.


============================================================
7. UPDATE PRODUCT 20 - DECREASE STOCK
============================================================

Original stock of Product 20:

30

Decrease stock by 1:

db.products.updateOne(
    { productId: 20 },
    { $inc: { stock: -1 } }
)

After update:

stock = 29

$inc is used to increase or decrease a numeric value.

Increase example:

db.products.updateOne(
    { productId: 20 },
    { $inc: { stock: 5 } }
)

Decrease example:

db.products.updateOne(
    { productId: 20 },
    { $inc: { stock: -1 } }
)


============================================================
8. ADD "Sale" TO PRODUCT 20 TAGS
============================================================

Original tags:

["electronics", "featured"]

Add "Sale":

db.products.updateOne(
    { productId: 20 },
    { $push: { tags: "Sale" } }
)

After update:

["electronics", "featured", "Sale"]

$push adds a new value to an array.


============================================================
9. $addToSet
============================================================

$addToSet is also used to add values to an array.

Difference:

$push
- Adds the value every time.
- Duplicate values are allowed.

$addToSet
- Adds the value only if it does not already exist.
- Prevents duplicate values.

Example:

db.products.updateOne(
    { productId: 20 },
    { $addToSet: { tags: "Sale" } }
)


============================================================
10. UPDATE MANY DOCUMENTS
============================================================

updateMany() is used when multiple documents need to be
updated.

Example:

db.products.updateMany(
    { category: "Mobile" },
    { $set: { price: 14999 } }
)

This changes the price of all products whose category is
"Mobile".

Important:

db.products.updateMany(
    {},
    { $set: { price: 14999 } }
)

An empty filter {} matches all documents.


============================================================
11. CHECK UPDATED PRODUCT 20
============================================================

Command:

db.products.findOne({ productId: 20 })


Final Product 20:

{
    productId: 20,
    productName: "Product 20",
    category: "Laptop",
    brand: "HP",
    price: 14999,
    stock: 29,
    rating: 4,
    inStock: false,

    tags: [
        "electronics",
        "featured",
        "Sale"
    ],

    seller: {
        sellerId: 1020,
        sellerName: "Seller 20"
    },

    createdAt: ISODate(...)
}


============================================================
12. INSERT ONE DOCUMENT
============================================================

insertOne() is used to insert a single document.

Example:

db.codex.insertOne({
    name: "Radhe",
    age: 20,
    branch: "AI & DS"
})


============================================================
13. INSERT MULTIPLE DOCUMENTS
============================================================

insertMany() is used to insert multiple documents at once.

Example:

db.BadStudents.insertMany([
    {
        name: "Aman",
        age: 21,
        branch: "CSE"
    },
    {
        name: "Rahul",
        age: 20,
        branch: "IT"
    },
    {
        name: "Priya",
        age: 21,
        branch: "AI & DS"
    },
    {
        name: "Neha",
        age: 20,
        branch: "ECE"
    }
])


============================================================
14. FIND DOCUMENTS
============================================================

Find all documents:

db.BadStudents.find()

Find one document:

db.BadStudents.findOne()

Find a specific document:

db.BadStudents.findOne({ name: "Radhe" })


============================================================
15. COLLECTION WITH SPACE IN NAME
============================================================

If a collection name contains a space, use bracket notation.

Example:

db["Bad Students"].find()

Insert into it:

db["Bad Students"].insertOne({
    name: "Radhe",
    age: 20,
    branch: "AI & DS"
})


Do NOT write:

db.Bad Students.find()

Correct:

db["Bad Students"].find()


============================================================
16. RENAME COLLECTION
============================================================

Rename:

Bad Students

to:

BadStudents

Command:

db["Bad Students"].renameCollection("BadStudents")

Check:

show collections


============================================================
17. MERGE TWO COLLECTIONS
============================================================

Copy documents from:

Bad Students

to:

BadStudents

Command:

db["Bad Students"].find().forEach(function(doc) {
    db.BadStudents.insertOne(doc)
})

Check the merged collection:

db.BadStudents.find()

Count documents:

db.BadStudents.countDocuments()


============================================================
18. DELETE COLLECTION
============================================================

To delete the old collection:

db["Bad Students"].drop()

Check:

show collections


============================================================
19. DELETE RADH COLLECTION
============================================================

A collection named RADH was created accidentally.

Check its data:

db.RADH.find()

Delete the complete collection:

db.RADH.drop()

Check collections:

show collections


============================================================
20. UPDATE ONE DOCUMENT
============================================================

Example using the codex collection:

db.codex.updateOne(
    { name: "Radhe" },
    { $set: { age: 23 } }
)

This changes:

age: 20

to:

age: 23


============================================================
21. UPDATE PRODUCT USING PRODUCT ID
============================================================

Example:

db.products.updateOne(
    { productId: 20 },
    { $set: { price: 14999 } }
)

Filter:

{ productId: 20 }

Update:

{ $set: { price: 14999 } }


============================================================
22. IMPORTANT UPDATE OPERATORS
============================================================

$set
Used to set/change a field value.

Example:

{ $set: { price: 14999 } }


$inc
Used to increase or decrease numeric values.

Example:

{ $inc: { stock: 1 } }

Decrease:

{ $inc: { stock: -1 } }


$push
Adds a value to an array.

Example:

{ $push: { tags: "Sale" } }


$addToSet
Adds a value to an array only if it does not already exist.

Example:

{ $addToSet: { tags: "Sale" } }


$unset
Removes a field from a document.

Example:

{ $unset: { rating: "" } }


$rename
Renames a field.

Example:

{ $rename: { oldField: "newField" } }


$pop
Removes an element from an array.

Example:

{ $pop: { tags: 1 } }

1 = removes the last element
-1 = removes the first element


$pull
Removes matching values from an array.

Example:

{ $pull: { tags: "Sale" } }


============================================================
23. DELETE DOCUMENTS
============================================================

Delete one document:

db.products.deleteOne(
    { productId: 20 }
)

Delete multiple documents:

db.products.deleteMany(
    { category: "Mouse" }
)


============================================================
24. QUERY OPERATORS
============================================================

Greater than:

{ price: { $gt: 10000 } }


Less than:

{ price: { $lt: 10000 } }


Greater than or equal to:

{ price: { $gte: 10000 } }


Less than or equal to:

{ price: { $lte: 10000 } }


Not equal:

{ brand: { $ne: "HP" } }


============================================================
25. ARRAY QUERY / LOGICAL OPERATORS
============================================================

OR:

db.products.find({
    $or: [
        { brand: "HP" },
        { brand: "Dell" }
    ]
})


AND:

db.products.find({
    $and: [
        { category: "Laptop" },
        { price: { $gt: 5000 } }
    ]
})


============================================================
26. COUNT DOCUMENTS
============================================================

Count all products:

db.products.countDocuments()

Count products with a condition:

db.products.countDocuments({
    category: "Laptop"
})


============================================================
27. SORT
============================================================

Sort price in ascending order:

db.products.find().sort({ price: 1 })

Sort price in descending order:

db.products.find().sort({ price: -1 })


1  = ascending
-1 = descending


============================================================
28. LIMIT
============================================================

Display only 5 products:

db.products.find().limit(5)


============================================================
29. PROJECTION
============================================================

Display only productName and price:

db.products.find(
    {},
    {
        productName: 1,
        price: 1
    }
)

1 means include the field.


============================================================
30. IMPORTANT MONGODB CONCEPTS LEARNED
============================================================

MongoDB structure:

Database
    ↓
Collection
    ↓
Document
    ↓
Fields


MongoDB comparison:

MySQL              MongoDB
--------------------------------
Database            Database
Table               Collection
Row                 Document
Column              Field


MongoDB stores documents in BSON format.

JSON is a text-based data format commonly used for data
representation.

BSON means Binary JSON and is the format MongoDB uses for
storing documents internally.

MongoDB documents can contain:
- Strings
- Numbers
- Boolean
- Arrays
- Embedded/Nested documents
- Dates
- ObjectId


============================================================
31. METHODS / OPERATORS COVERED
============================================================

Database / Collection:
1. db
2. show dbs
3. use
4. show collections
5. createCollection()
6. drop()
7. renameCollection()

Insert:
8. insertOne()
9. insertMany()

Read:
10. find()
11. findOne()
12. countDocuments()

Update:
13. updateOne()
14. updateMany()

Update operators:
15. $set
16. $inc
17. $push
18. $addToSet
19. $unset
20. $rename
21. $pop
22. $pull

Delete:
23. deleteOne()
24. deleteMany()

Query operators:
25. $gt
26. $lt
27. $gte
28. $lte
29. $ne
30. $or
31. $and

Other:
32. sort()
33. limit()
34. Projection


============================================================
32. PRODUCT 20 FINAL RESULT
============================================================

Product ID:
20

Product Name:
Product 20

Category:
Laptop

Brand:
HP

Price:
14999

Stock:
29

Rating:
4

In Stock:
false

Tags:
electronics
featured
Sale

Seller ID:
1020

Seller Name:
Seller 20


============================================================
                  END OF MONGODB PRACTICE
============================================================
