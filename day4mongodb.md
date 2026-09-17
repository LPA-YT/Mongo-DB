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
Atlas atlas-104b3m-shard-0 [primary] test> use test
already on db test
Atlas atlas-104b3m-shard-0 [primary] test> db.createCollection("product")
{ ok: 1 }
use shopDB

db.createCollection("items")

const categories = [
    "Gadgets",
    "Smartphones",
    "Computers",
    "Fashion",
    "Stationery",
    "Home Decor",
    "Footwear",
    "Accessories",
    "Kitchen",
    "Fitness"
];

const brands = [
    "Google",
    "Xiaomi",
    "Asus",
    "Acer",
    "Reebok",
    "Casio",
    "JBL",
    "Boat",
    "Philips",
    "Realme"
];

const cities = [
    "Jaipur",
    "Delhi",
    "Mumbai",
    "Pune",
    "Ahmedabad",
    "Surat",
    "Lucknow",
    "Indore",
    "Bhopal",
    "Udaipur"
];

const labels = [
    "latest",
    "popular",
    "sale",
    "premium",
    "limited",
    "recommended",
    "featured",
    "value"
];

const paymentOptions = [
    "UPI",
    "Credit Card",
    "Debit Card",
    "Net Banking",
    "COD"
];

let items = [];

for (let i = 101; i <= 5100; i++) {

    let category = categories[i % categories.length];
    let brand = brands[(i + 3) % brands.length];
    let city = cities[(i + 5) % cities.length];

    let price = Math.floor(Math.random() * 75000) + 2000;
    let stock = Math.floor(Math.random() * 25) + 1;

    let rating = Number(
        (Math.random() * 3.5 + 1.5).toFixed(1)
    );

    let itemLabels = [
        labels[i % labels.length],
        labels[(i + 3) % labels.length]
    ];

    let item = {
        itemCode: i,

        title: brand + " Item " + i,

        category: category,

        brand: brand,

        price: price,

        stock: stock,

        rating: rating,

        details:
            "A reliable " +
            category +
            " item manufactured by " +
            brand +
            " with useful features and dependable performance.",

        labels: itemLabels,

        vendor: {
            vendorCode: 2000 + (i % 80),
            vendorName: "Vendor " + (i % 80),
            city: city
        },

        location: {
            type: "Point",
            coordinates: [
                74.75 + (Math.random() * 0.6),
                26.75 + (Math.random() * 0.6)
            ]
        },

        paymentOptions: paymentOptions,

        available: i % 6 !== 0,

        addedOn: new Date(
            2025,
            i % 12,
            (i % 27) + 1
        )
    };

    if (i % 4 === 0) {
        item.contactEmail =
            "buyer" + i + "@maildemo.com";
    }

    if (i % 5 === 0) {
        item.offer =
            Math.floor(Math.random() * 35) + 10;
    }

    items.push(item);

    if (items.length === 400) {
        db.items.insertMany(items);
        items = [];
    }
}

if (items.length > 0) {
    db.items.insertMany(items);
}

print("5000 items inserted successfully!");

db.items.countDocuments()
