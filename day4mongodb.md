Microsoft Windows [Version 10.0.26200.9457]
(c) Microsoft Corporation. All rights reserved.

C:\Users\HP>mongosh "mongodb+srv://cluster0.u5gi0my.mongodb.net/" --apiVersion 1 --username vasanth970399_db_user
Enter password: ****************
Current Mongosh Log ID: 6aab707f1302b4034a49df95
Connecting to:          mongodb+srv://<credentials>@cluster0.u5gi0my.mongodb.net/?appName=mongosh+2.10.0
Using MongoDB:          8.0.32 (API Version 1)
Using Mongosh:          2.10.0
mongosh 2.11.1 is available for download: https://www.mongodb.com/try/download/shell

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/

Atlas atlas-104b3m-shard-0 [primary] test> show dbs
PCEA24AD005            3.31 MiB
PCEA24AD006            2.23 MiB
PCEA24AD008            3.00 MiB
PCEA24AD026            8.00 KiB
PCEA24AD028            2.35 MiB
PCEA24AD032            4.32 MiB
PCEA24AD043            3.47 MiB
PCEA24AD051            3.90 MiB
PCEA24CA001            3.21 MiB
PCEA24CA016            2.36 MiB
PCEA24CA019            2.61 MiB
PCEA24CA020            3.20 MiB
PCEA24CA055            2.29 MiB
PCEA24CA059            2.25 MiB
PCEA24CY001            2.22 MiB
PCEA24CY002          144.00 KiB
PCEA24CY005            2.33 MiB
PCEA24CY020            2.89 MiB
PCEA24CY022           72.00 KiB
PCEA24CY023            2.41 MiB
PCEA24CY024            2.46 MiB
PCEA24CY031            5.46 MiB
PCEA24CY033           72.00 KiB
PCEA24CY046            2.59 MiB
PCEA24CY049           72.00 KiB
PCEA24CY055           88.00 KiB
PCEA24CY064          152.00 KiB
PCEA24IT009           80.00 KiB
PCEA24IT011            5.31 MiB
PCEA24IT024            8.00 KiB
PCEA24IT032           80.00 KiB
PCEA24IT036          152.00 KiB
PCEA24IT042            2.24 MiB
PCEA24IT047          160.00 KiB
PCEA24IT049           80.00 KiB
PCEA24IT051           80.00 KiB
PCEA24IT055            2.52 MiB
PCEA24IT056            8.00 KiB
PCEA24IT058           80.00 KiB
PCEA25AD803            2.16 MiB
ProductDB             72.00 KiB
Radhe                 72.00 KiB
Sample01               8.00 KiB
Sample1                3.95 MiB
aggex                  2.20 MiB
cmd                    6.79 MiB
exam_hall_optimizer  992.00 KiB
onlineStoreDB          2.36 MiB
pcea24cy011            2.30 MiB
pcea24cy037           72.00 KiB
pcea24cy041            2.14 MiB
sample02             144.00 KiB
test                   7.36 MiB
admin                       0 B
local                       0 B
Atlas atlas-104b3m-shard-0 [primary] test> use PCEA24AD043 
already on db PCEA24AD043
Atlas atlas-104b3m-shard-0 [primary] test> db.createCollection("product")
{ ok: 1 }
Atlas atlas-104b3m-shard-0 [primary] test> show collections
aggex
auditlogs
PCEA24CA028
PCEA24AD043
product
products
students
Atlas atlas-104b3m-shard-0 [primary] test> const categories = [
|     "Electronics",
|     "Mobiles",
|     "Laptops",
|     "Clothing",
|     "Books",
|     "Furniture",
|     "Shoes",
|     "Accessories",
|     "Home Appliances",
|     "Sports"
| ];
|
| const brands = [
|     "Apple",
|     "Samsung",
|     "Dell",
|     "HP",
|     "Lenovo",
|     "Sony",
|     "Nike",
|     "Adidas",
|     "Puma",
|     "OnePlus"
| ];
|
| const cities = [
|     "Chennai",
|     "Bangalore",
|     "Hyderabad",
|     "Coimbatore",
|     "Salem",
|     "Erode",
|     "Tiruchengode",
|     "Madurai",
|     "Trichy",
|     "Pondicherry"
| ];
|
| const tags = [
|     "new",
|     "popular",
|     "discount",
|     "premium",
|     "bestseller",
|     "trending",
|     "featured",
|     "budget"
| ];
|
| const paymentMethods = [
|     "UPI",
|     "Credit Card",
|     "Debit Card",
|     "Cash",
|     "Net Banking"
| ];
|
|
| // Array to temporarily store documents
| let products = [];
|
|
| // Generate 5000 documents
| for (let i = 1; i <= 5000; i++) {
|
|     let category = categories[i % categories.length];
|
|     let brand = brands[i % brands.length];
|
|     let city = cities[i % cities.length];
|
|     let price = Math.floor(Math.random() * 90000) + 1000;
|
|     let quantity = Math.floor(Math.random() * 10) + 1;
|
|     let rating = Number(
|         (Math.random() * 4 + 1).toFixed(1)
|     );
|
|
|     let productTags = [
|         tags[i % tags.length],
|         tags[(i + 2) % tags.length]
|     ];
|
|
|     let product = {
|
|         productId: i,
|
|         name: brand + " Product " + i,
|
|         category: category,
|
|         brand: brand,
|
|         price: price,
|
|         quantity: quantity,
|
|         rating: rating,
|
|         description:
|             "This is a high quality " +
|             category +
|             " product from " +
|             brand +
|             " with excellent features and performance.",
|
|         tags: productTags,
|
|
|         seller: {
|
|             sellerId: 1000 + (i % 100),
|
|             name: "Seller " + (i % 100),
|
|             city: city
|         },
|
|
|         location: {
|
|             type: "Point",
|
|             coordinates: [
|                 76.95 + (Math.random() * 0.5),
|                 11.00 + (Math.random() * 0.5)
|             ]
|         },
|         paymentMethods: paymentMethods,
|         isActive: i % 5 !== 0,
|         createdAt: new Date(
|             2024,
|             i % 12,
|             (i % 28) + 1
|         )
|     };
|     // Add email to some documents
|     // Useful for Sparse Index
|     if (i % 3 === 0) {
|
|         product.email =
|             "customer" + i + "@example.com";
|     }
|     // Add discount to some documents
|     // Useful for Partial Index
|     if (i % 4 === 0) {
|
|         product.discount =
|             Math.floor(Math.random() * 40) + 5;
|     }
|     // Add document to array
|     products.push(product);
|     // Insert in batches of 500
|     if (products.length === 500) {
|
|         db.product.insertMany(products);
|
|         products = [];
|     }
| }
| // Insert remaining documents
| if (products.length > 0) {
|
|     db.product.insertMany(products);
| }
| print("5000 documents inserted successfully!");
db.product.countDocuments()
5000 documents inserted successfully!

Atlas atlas-104b3m-shard-0 [primary] test> db.product.countDocuments()
5000
Atlas atlas-104b3m-shard-0 [primary] test> db.product.findOne()
{
  _id: ObjectId('6aab71c51302b4034a49df96'),
  productId: 1,
  name: 'Samsung Product 1',
  category: 'Mobiles',
  brand: 'Samsung',
  price: 17968,
  quantity: 1,
  rating: 4.6,
  description: 'This is a high quality Mobiles product from Samsung with excellent features and performance.',
  tags: [ 'popular', 'premium' ],
  seller: { sellerId: 1001, name: 'Seller 1', city: 'Bangalore' },
  location: {
    type: 'Point',
    coordinates: [ 77.00293476335689, 11.00790458802841 ]
  },
  paymentMethods: [ 'UPI', 'Credit Card', 'Debit Card', 'Cash', 'Net Banking' ],
  isActive: true,
  createdAt: ISODate('2024-02-01T18:30:00.000Z')
}
Atlas atlas-104b3m-shard-0 [primary] test> db.product.dropIndex({"price_1"})
Uncaught:
SyntaxError: Unexpected token (1:31)

> 1 | db.product.dropIndex({"price_1"})
    |                                ^
  2 |

Atlas atlas-104b3m-shard-0 [primary] test> db.product.dropIndex("price_1")
MongoServerError[IndexNotFound]: index not found with name [price_1]
Atlas atlas-104b3m-shard-0 [primary] test> db.product.createIndex({ category: 1 })
category_1
Atlas atlas-104b3m-shard-0 [primary] test> use ecomDB
| show collections
| db.product.countDocuments()
switched to db ecomDB
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.find({ price: { $gt: 50000 } }).explain("executionStats")
{
  explainVersion: '1',
  queryPlanner: {
    namespace: 'ecomDB.product',
    parsedQuery: { price: { '$gt': 50000 } },
    indexFilterSet: false,
    optimizationTimeMillis: 0,
    maxIndexedOrSolutionsReached: false,
    maxIndexedAndSolutionsReached: false,
    maxScansToExplodeReached: false,
    prunedSimilarIndexes: false,
    winningPlan: { isCached: false, stage: 'EOF' },
    rejectedPlans: []
  },
  executionStats: {
    executionSuccess: true,
    nReturned: 0,
    executionTimeMillis: 0,
    totalKeysExamined: 0,
    totalDocsExamined: 0,
    executionStages: {
      isCached: false,
      stage: 'EOF',
      nReturned: 0,
      executionTimeMillisEstimate: 0,
      works: 1,
      advanced: 0,
      needTime: 0,
      needYield: 0,
      saveState: 0,
      restoreState: 0,
      isEOF: 1
    }
  },
  queryShapeHash: '9A013AA107331F25CA7380F6D62683FBFEAC7A6644C0910D35392F13B0135011',
  command: {
    find: 'product',
    filter: { price: { '$gt': 50000 } },
    '$db': 'ecomDB'
  },
  serverInfo: {
    host: 'ac-28kwaq2-shard-00-01.u5gi0my.mongodb.net',
    port: 27017,
    version: '8.0.32',
    gitVersion: 'f9eb55a7cc900f33a722a5b32a0fdbf54385c749'
  },
  serverParameters: {
    internalQueryFacetBufferSizeBytes: 104857600,
    internalQueryFacetMaxOutputDocSizeBytes: 104857600,
    internalLookupStageIntermediateDocumentMaxSizeBytes: 16793600,
    internalDocumentSourceGroupMaxMemoryBytes: 104857600,
    internalQueryMaxBlockingSortMemoryUsageBytes: 33554432,
    internalQueryProhibitBlockingMergeOnMongoS: 0,
    internalQueryMaxAddToSetBytes: 104857600,
    internalDocumentSourceSetWindowFieldsMaxMemoryBytes: 104857600,
    internalQueryFrameworkControl: 'trySbeRestricted',
    internalQueryPlannerIgnoreIndexWithCollationForRegex: 1
  },
  ok: 1,
  '$clusterTime': {
    clusterTime: Timestamp({ t: 1789621137, i: 8 }),
    signature: {
      hash: Binary.createFromBase64('/AIa+xl2/lRSBO5aILnlDVBhlcA=', 0),
      keyId: Long('7634928556237127691')
    }
  },
  operationTime: Timestamp({ t: 1789621137, i: 8 })
}
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.createIndex({ price: 1 })
price_1
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.find({ price: { $gt: 50000 } }).explain("executionStats")
{
  explainVersion: '1',
  queryPlanner: {
    namespace: 'ecomDB.product',
    parsedQuery: { price: { '$gt': 50000 } },
    indexFilterSet: false,
    queryHash: '8E1D451A',
    planCacheShapeHash: '8E1D451A',
    planCacheKey: 'F4407A58',
    optimizationTimeMillis: 0,
    maxIndexedOrSolutionsReached: false,
    maxIndexedAndSolutionsReached: false,
    maxScansToExplodeReached: false,
    prunedSimilarIndexes: false,
    winningPlan: {
      isCached: false,
      stage: 'FETCH',
      inputStage: {
        stage: 'IXSCAN',
        keyPattern: { price: 1 },
        indexName: 'price_1',
        isMultiKey: false,
        multiKeyPaths: { price: [] },
        isUnique: false,
        isSparse: false,
        isPartial: false,
        indexVersion: 2,
        direction: 'forward',
        indexBounds: { price: [ '(50000, inf.0]' ] }
      }
    },
    rejectedPlans: []
  },
  executionStats: {
    executionSuccess: true,
    nReturned: 0,
    executionTimeMillis: 0,
    totalKeysExamined: 0,
    totalDocsExamined: 0,
    executionStages: {
      isCached: false,
      stage: 'FETCH',
      nReturned: 0,
      executionTimeMillisEstimate: 0,
      works: 1,
      advanced: 0,
      needTime: 0,
      needYield: 0,
      saveState: 0,
      restoreState: 0,
      isEOF: 1,
      docsExamined: 0,
      alreadyHasObj: 0,
      inputStage: {
        stage: 'IXSCAN',
        nReturned: 0,
        executionTimeMillisEstimate: 0,
        works: 1,
        advanced: 0,
        needTime: 0,
        needYield: 0,
        saveState: 0,
        restoreState: 0,
        isEOF: 1,
        keyPattern: { price: 1 },
        indexName: 'price_1',
        isMultiKey: false,
        multiKeyPaths: { price: [] },
        isUnique: false,
        isSparse: false,
        isPartial: false,
        indexVersion: 2,
        direction: 'forward',
        indexBounds: { price: [ '(50000, inf.0]' ] },
        keysExamined: 0,
        seeks: 1,
        dupsTested: 0,
        dupsDropped: 0
      }
    }
  },
  queryShapeHash: '9A013AA107331F25CA7380F6D62683FBFEAC7A6644C0910D35392F13B0135011',
  command: {
    find: 'product',
    filter: { price: { '$gt': 50000 } },
    '$db': 'ecomDB'
  },
  serverInfo: {
    host: 'ac-28kwaq2-shard-00-01.u5gi0my.mongodb.net',
    port: 27017,
    version: '8.0.32',
    gitVersion: 'f9eb55a7cc900f33a722a5b32a0fdbf54385c749'
  },
  serverParameters: {
    internalQueryFacetBufferSizeBytes: 104857600,
    internalQueryFacetMaxOutputDocSizeBytes: 104857600,
    internalLookupStageIntermediateDocumentMaxSizeBytes: 16793600,
    internalDocumentSourceGroupMaxMemoryBytes: 104857600,
    internalQueryMaxBlockingSortMemoryUsageBytes: 33554432,
    internalQueryProhibitBlockingMergeOnMongoS: 0,
    internalQueryMaxAddToSetBytes: 104857600,
    internalDocumentSourceSetWindowFieldsMaxMemoryBytes: 104857600,
    internalQueryFrameworkControl: 'trySbeRestricted',
    internalQueryPlannerIgnoreIndexWithCollationForRegex: 1
  },
  ok: 1,
  '$clusterTime': {
    clusterTime: Timestamp({ t: 1789621166, i: 9 }),
    signature: {
      hash: Binary.createFromBase64('azIY9tELP1JaNglly/EFc1BapOs=', 0),
      keyId: Long('7634928556237127691')
    }
  },
  operationTime: Timestamp({ t: 1789621166, i: 9 })
}
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { price: 1 }, name: 'price_1' }
]
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.find({
|     category: "Electronics",
|     price: { $gt: 50000 }
| }).explain("executionStats")
{
  explainVersion: '1',
  queryPlanner: {
    namespace: 'ecomDB.product',
    parsedQuery: {
      '$and': [
        { category: { '$eq': 'Electronics' } },
        { price: { '$gt': 50000 } }
      ]
    },
    indexFilterSet: false,
    queryHash: '4241127D',
    planCacheShapeHash: '4241127D',
    planCacheKey: 'E8901157',
    optimizationTimeMillis: 0,
    maxIndexedOrSolutionsReached: false,
    maxIndexedAndSolutionsReached: false,
    maxScansToExplodeReached: false,
    prunedSimilarIndexes: false,
    winningPlan: {
      isCached: false,
      stage: 'FETCH',
      filter: { category: { '$eq': 'Electronics' } },
      inputStage: {
        stage: 'IXSCAN',
        keyPattern: { price: 1 },
        indexName: 'price_1',
        isMultiKey: false,
        multiKeyPaths: { price: [] },
        isUnique: false,
        isSparse: false,
        isPartial: false,
        indexVersion: 2,
        direction: 'forward',
        indexBounds: { price: [ '(50000, inf.0]' ] }
      }
    },
    rejectedPlans: []
  },
  executionStats: {
    executionSuccess: true,
    nReturned: 0,
    executionTimeMillis: 0,
    totalKeysExamined: 0,
    totalDocsExamined: 0,
    executionStages: {
      isCached: false,
      stage: 'FETCH',
      filter: { category: { '$eq': 'Electronics' } },
      nReturned: 0,
      executionTimeMillisEstimate: 0,
      works: 1,
      advanced: 0,
      needTime: 0,
      needYield: 0,
      saveState: 0,
      restoreState: 0,
      isEOF: 1,
      docsExamined: 0,
      alreadyHasObj: 0,
      inputStage: {
        stage: 'IXSCAN',
        nReturned: 0,
        executionTimeMillisEstimate: 0,
        works: 1,
        advanced: 0,
        needTime: 0,
        needYield: 0,
        saveState: 0,
        restoreState: 0,
        isEOF: 1,
        keyPattern: { price: 1 },
        indexName: 'price_1',
        isMultiKey: false,
        multiKeyPaths: { price: [] },
        isUnique: false,
        isSparse: false,
        isPartial: false,
        indexVersion: 2,
        direction: 'forward',
        indexBounds: { price: [ '(50000, inf.0]' ] },
        keysExamined: 0,
        seeks: 1,
        dupsTested: 0,
        dupsDropped: 0
      }
    }
  },
  queryShapeHash: '980E90A9BFCB55DB85F0DA24BBF451FC97D965B27BB658E039F04A8E1FD338BF',
  command: {
    find: 'product',
    filter: { category: 'Electronics', price: { '$gt': 50000 } },
    '$db': 'ecomDB'
  },
  serverInfo: {
    host: 'ac-28kwaq2-shard-00-01.u5gi0my.mongodb.net',
    port: 27017,
    version: '8.0.32',
    gitVersion: 'f9eb55a7cc900f33a722a5b32a0fdbf54385c749'
  },
  serverParameters: {
    internalQueryFacetBufferSizeBytes: 104857600,
    internalQueryFacetMaxOutputDocSizeBytes: 104857600,
    internalLookupStageIntermediateDocumentMaxSizeBytes: 16793600,
    internalDocumentSourceGroupMaxMemoryBytes: 104857600,
    internalQueryMaxBlockingSortMemoryUsageBytes: 33554432,
    internalQueryProhibitBlockingMergeOnMongoS: 0,
    internalQueryMaxAddToSetBytes: 104857600,
    internalDocumentSourceSetWindowFieldsMaxMemoryBytes: 104857600,
    internalQueryFrameworkControl: 'trySbeRestricted',
    internalQueryPlannerIgnoreIndexWithCollationForRegex: 1
  },
  ok: 1,
  '$clusterTime': {
    clusterTime: Timestamp({ t: 1789621197, i: 9 }),
    signature: {
      hash: Binary.createFromBase64('wmq2wJROSKqaKqNCO4Mf7sSSpRU=', 0),
      keyId: Long('7634928556237127691')
    }
  },
  operationTime: Timestamp({ t: 1789621197, i: 9 })
}
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.createIndex({
|     category: 1,
|     price: -1
| })
category_1_price_-1
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.find({
|     category: "Electronics",
|     price: { $gt: 50000 }
| }).explain("executionStats")
{
  explainVersion: '1',
  queryPlanner: {
    namespace: 'ecomDB.product',
    parsedQuery: {
      '$and': [
        { category: { '$eq': 'Electronics' } },
        { price: { '$gt': 50000 } }
      ]
    },
    indexFilterSet: false,
    queryHash: '4241127D',
    planCacheShapeHash: '4241127D',
    planCacheKey: '98B027FB',
    optimizationTimeMillis: 0,
    maxIndexedOrSolutionsReached: false,
    maxIndexedAndSolutionsReached: false,
    maxScansToExplodeReached: false,
    prunedSimilarIndexes: false,
    winningPlan: {
      isCached: false,
      stage: 'FETCH',
      inputStage: {
        stage: 'IXSCAN',
        keyPattern: { category: 1, price: -1 },
        indexName: 'category_1_price_-1',
        isMultiKey: false,
        multiKeyPaths: { category: [], price: [] },
        isUnique: false,
        isSparse: false,
        isPartial: false,
        indexVersion: 2,
        direction: 'forward',
        indexBounds: {
          category: [ '["Electronics", "Electronics"]' ],
          price: [ '[inf.0, 50000)' ]
        }
      }
    },
    rejectedPlans: [
      {
        isCached: false,
        stage: 'FETCH',
        filter: { category: { '$eq': 'Electronics' } },
        inputStage: {
          stage: 'IXSCAN',
          keyPattern: { price: 1 },
          indexName: 'price_1',
          isMultiKey: false,
          multiKeyPaths: { price: [] },
          isUnique: false,
          isSparse: false,
          isPartial: false,
          indexVersion: 2,
          direction: 'forward',
          indexBounds: { price: [ '(50000, inf.0]' ] }
        }
      }
    ]
  },
  executionStats: {
    executionSuccess: true,
    nReturned: 0,
    executionTimeMillis: 0,
    totalKeysExamined: 0,
    totalDocsExamined: 0,
    executionStages: {
      isCached: false,
      stage: 'FETCH',
      nReturned: 0,
      executionTimeMillisEstimate: 0,
      works: 2,
      advanced: 0,
      needTime: 0,
      needYield: 0,
      saveState: 0,
      restoreState: 0,
      isEOF: 1,
      docsExamined: 0,
      alreadyHasObj: 0,
      inputStage: {
        stage: 'IXSCAN',
        nReturned: 0,
        executionTimeMillisEstimate: 0,
        works: 1,
        advanced: 0,
        needTime: 0,
        needYield: 0,
        saveState: 0,
        restoreState: 0,
        isEOF: 1,
        keyPattern: { category: 1, price: -1 },
        indexName: 'category_1_price_-1',
        isMultiKey: false,
        multiKeyPaths: { category: [], price: [] },
        isUnique: false,
        isSparse: false,
        isPartial: false,
        indexVersion: 2,
        direction: 'forward',
        indexBounds: {
          category: [ '["Electronics", "Electronics"]' ],
          price: [ '[inf.0, 50000)' ]
        },
        keysExamined: 0,
        seeks: 1,
        dupsTested: 0,
        dupsDropped: 0
      }
    }
  },
  queryShapeHash: '980E90A9BFCB55DB85F0DA24BBF451FC97D965B27BB658E039F04A8E1FD338BF',
  command: {
    find: 'product',
    filter: { category: 'Electronics', price: { '$gt': 50000 } },
    '$db': 'ecomDB'
  },
  serverInfo: {
    host: 'ac-28kwaq2-shard-00-01.u5gi0my.mongodb.net',
    port: 27017,
    version: '8.0.32',
    gitVersion: 'f9eb55a7cc900f33a722a5b32a0fdbf54385c749'
  },
  serverParameters: {
    internalQueryFacetBufferSizeBytes: 104857600,
    internalQueryFacetMaxOutputDocSizeBytes: 104857600,
    internalLookupStageIntermediateDocumentMaxSizeBytes: 16793600,
    internalDocumentSourceGroupMaxMemoryBytes: 104857600,
    internalQueryMaxBlockingSortMemoryUsageBytes: 33554432,
    internalQueryProhibitBlockingMergeOnMongoS: 0,
    internalQueryMaxAddToSetBytes: 104857600,
    internalDocumentSourceSetWindowFieldsMaxMemoryBytes: 104857600,
    internalQueryFrameworkControl: 'trySbeRestricted',
    internalQueryPlannerIgnoreIndexWithCollationForRegex: 1
  },
  ok: 1,
  '$clusterTime': {
    clusterTime: Timestamp({ t: 1789621232, i: 2 }),
    signature: {
      hash: Binary.createFromBase64('ZzEXfGLjumkFWvNXisds+wtdGDY=', 0),
      keyId: Long('7634928556237127691')
    }
  },
  operationTime: Timestamp({ t: 1789621232, i: 2 })
}
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { price: 1 }, name: 'price_1' },
  { v: 2, key: { category: 1, price: -1 }, name: 'category_1_price_-1' }
]
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.createIndex({
|     tags: 1
| })
|
| db.product.find({
|     tags: "bestseller"
| }).explain("executionStats")
|
| db.product.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { price: 1 }, name: 'price_1' },
  { v: 2, key: { category: 1, price: -1 }, name: 'category_1_price_-1' },
  { v: 2, key: { tags: 1 }, name: 'tags_1' }
]
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.createIndex({
|     description: "text"
| })
|
| db.product.find({
|     $text: {
|         $search: "Samsung"
|     }
| }).explain("executionStats")
|
| db.product.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { price: 1 }, name: 'price_1' },
  { v: 2, key: { category: 1, price: -1 }, name: 'category_1_price_-1' },
  { v: 2, key: { tags: 1 }, name: 'tags_1' },
  {
    v: 2,
    key: { _fts: 'text', _ftsx: 1 },
    name: 'description_text',
    weights: { description: 1 },
    default_language: 'english',
    language_override: 'language',
    textIndexVersion: 3
  }
]
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.createIndex({
|     productId: "hashed"
| })
|
| db.product.find({
|     productId: 101
| })
|
| db.product.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { price: 1 }, name: 'price_1' },
  { v: 2, key: { category: 1, price: -1 }, name: 'category_1_price_-1' },
  { v: 2, key: { tags: 1 }, name: 'tags_1' },
  {
    v: 2,
    key: { _fts: 'text', _ftsx: 1 },
    name: 'description_text',
    weights: { description: 1 },
    default_language: 'english',
    language_override: 'language',
    textIndexVersion: 3
  },
  { v: 2, key: { productId: 'hashed' }, name: 'productId_hashed' }
]
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.createIndex({
|     location: "2dsphere"
| })
|
| db.product.find({
|     location: {
|         $near: {
|             $geometry: {
|                 type: "Point",
|                 coordinates: [77.0, 11.1]
|             },
|             $maxDistance: 10000
|         }
|     }
| })
|
| db.product.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { price: 1 }, name: 'price_1' },
  { v: 2, key: { category: 1, price: -1 }, name: 'category_1_price_-1' },
  { v: 2, key: { tags: 1 }, name: 'tags_1' },
  {
    v: 2,
    key: { _fts: 'text', _ftsx: 1 },
    name: 'description_text',
    weights: { description: 1 },
    default_language: 'english',
    language_override: 'language',
    textIndexVersion: 3
  },
  { v: 2, key: { productId: 'hashed' }, name: 'productId_hashed' },
  {
    v: 2,
    key: { location: '2dsphere' },
    name: 'location_2dsphere',
    '2dsphereIndexVersion': 3
  }
]
Atlas atlas-104b3m-shard-0 [primary] ecomDB> db.product.createIndex(
|     { email: 1 },
|     {
|         unique: true,
|         sparse: true
|     }
| )
|
| db.product.getIndexes()
|
| db.product.findOne({
|     email: "customer3@example.com"
| })
null
Atlas atlas-104b3m-shard-0 [primary] ecomDB>
