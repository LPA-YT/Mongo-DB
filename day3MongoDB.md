db.createCollection("Aggex")

const categories = [
    "Electronics",
    "Mobiles",
    "Laptops",
    "Home Appliances",
    "Fashion",
    "Books",
    "Sports",
    "Beauty",
    "Grocery",
    "Furniture"
];

const subCategories = {
    "Electronics": ["Headphones", "Smartwatch", "Camera", "Speaker"],
    "Mobiles": ["Android", "iPhone", "Feature Phone"],
    "Laptops": ["Gaming", "Business", "Student"],
    "Home Appliances": ["Refrigerator", "Washing Machine", "Microwave"],
    "Fashion": ["Men", "Women", "Kids"],
    "Books": ["Programming", "Fiction", "Education"],
    "Sports": ["Cricket", "Football", "Fitness"],
    "Beauty": ["Skincare", "Haircare", "Makeup"],
    "Grocery": ["Snacks", "Beverages", "Staples"],
    "Furniture": ["Chair", "Table", "Sofa"]
};

const brands = [
    "Samsung",
    "Apple",
    "Sony",
    "LG",
    "HP",
    "Dell",
    "Lenovo",
    "Nike",
    "Adidas",
    "Boat",
    "OnePlus",
    "AmazonBasics"
];

const cities = [
    "Chennai",
    "Coimbatore",
    "Bangalore",
    "Hyderabad",
    "Mumbai",
    "Delhi",
    "Pune",
    "Kochi",
    "Kolkata",
    "Ahmedabad"
];

const states = [
    "Tamil Nadu",
    "Karnataka",
    "Telangana",
    "Maharashtra",
    "Delhi",
    "Kerala",
    "West Bengal",
    "Gujarat"
];

const paymentMethods = [
    "UPI",
    "Credit Card",
    "Debit Card",
    "Net Banking",
    "Cash on Delivery"
];

const orderStatuses = [
    "Delivered",
    "Shipped",
    "Processing",
    "Cancelled",
    "Returned"
];

const sellers = [
    "RetailHub",
    "TechWorld",
    "MegaStore",
    "DigitalMart",
    "SmartShop",
    "PrimeRetail"
];

const tags = [
    "new",
    "popular",
    "trending",
    "premium",
    "budget",
    "best-seller",
    "discount",
    "limited-stock"
];


// Store documents temporarily
let documents = [];


// Generate 5000 documents
for (let i = 1; i <= 5000; i++) {

    const category =
        categories[Math.floor(Math.random() * categories.length)];

    const subCategory =
        subCategories[category][
            Math.floor(Math.random() * subCategories[category].length)
        ];

    const brand =
        brands[Math.floor(Math.random() * brands.length)];

    const city =
        cities[Math.floor(Math.random() * cities.length)];

    const state =
        states[Math.floor(Math.random() * states.length)];

    const paymentMethod =
        paymentMethods[
            Math.floor(Math.random() * paymentMethods.length)
        ];

    const orderStatus =
        orderStatuses[
            Math.floor(Math.random() * orderStatuses.length)
        ];

    const seller =
        sellers[
            Math.floor(Math.random() * sellers.length)
        ];


    const quantity =
        Math.floor(Math.random() * 5) + 1;

    const price =
        Math.floor(Math.random() * 95000) + 500;

    const discount =
        Math.floor(Math.random() * 51);

    const discountedPrice =
        Math.round(
            price - (price * discount / 100)
        );

    const rating =
        Number(
            (Math.random() * 4 + 1).toFixed(1)
        );

    const stock =
        Math.floor(Math.random() * 500);


    // Generate 2 random tags
    const selectedTags = [];

    for (let j = 0; j < 2; j++) {

        selectedTags.push(
            tags[Math.floor(Math.random() * tags.length)]
        );
    }


    // Random date between 2024 and 2026
    const startDate =
        new Date("2024-01-01").getTime();

    const endDate =
        new Date("2026-08-25").getTime();

    const randomDate =
        new Date(
            startDate +
            Math.random() * (endDate - startDate)
        );


    // Create document
    const product = {

        productId:
            "PROD" + String(i).padStart(5, "0"),

        productName:
            brand + " " + subCategory + " " + i,

        category: category,

        subCategory: subCategory,

        brand: brand,

        price: price,

        discountPercentage: discount,

        discountedPrice: discountedPrice,

        quantity: quantity,

        revenue:
            discountedPrice * quantity,

        rating: rating,

        reviewCount:
            Math.floor(Math.random() * 5000),

        stock: stock,

        inStock:
            stock > 0,


        seller: {

            name: seller,

            sellerRating:
                Number(
                    (Math.random() * 4 + 1).toFixed(1)
                )
        },


        customer: {

            customerId:
                "CUS" +
                String(
                    Math.floor(Math.random() * 1000) + 1
                ).padStart(4, "0"),

            city: city,

            state: state,

            age:
                Math.floor(Math.random() * 50) + 18
        },


        payment: {

            method: paymentMethod,

            transactionId:
                "TXN" +
                Math.random()
                    .toString(36)
                    .substring(2, 12)
        },


        orderStatus: orderStatus,

        orderDate: randomDate,

        tags: selectedTags,


        specifications: {

            warranty:
                (Math.floor(Math.random() * 3) + 1) +
                " years",

            color: [
                "Black",
                "White",
                "Blue",
                "Red",
                "Silver"
            ][Math.floor(Math.random() * 5)],

            weight:
                Number(
                    (Math.random() * 5 + 0.5).toFixed(2)
                )
        },


        isFeatured:
            Math.random() > 0.7,

        createdAt: new Date()
    };


    documents.push(product);


    // Insert every 500 documents
    if (documents.length === 500) {

        db.aggex.insertMany(documents);

        documents = [];
    }
}


if (documents.length > 0) {

    db.aggex.insertMany(documents);
}
print("5000 documents inserted successfully into aggex!");


db.aggex.aggregate([
    { $match: { category: "Books" } }])

db.aggex.aggregate([
  {
    $match: {
      price: { $gt: 50000 }
    }
  }
])

#All data with the price grater then 5000 in output

db.aggex.aggregate([
  {
    $match: {
      price: { $lt: 50000 }
    }
  }
])


#all data with price less then 5000 in output

db.aggex.aggregate([
  {
    $project: {
      _id: 0,
      productName: 1,
      price: 1
    }
  }
])

db.aggex.aggregate([
|   {
|     $project: {
|       _id: 0,
|       productName: 1,
|       price: 1
|     }
|   }
| ])
[
  { productName: 'AmazonBasics Men 1', price: 60472 },
  { productName: 'Samsung Business 2', price: 41620 },
  { productName: 'Apple Fitness 3', price: 47754 },
  { productName: 'LG Speaker 4', price: 46807 },
  { productName: 'Lenovo Speaker 5', price: 61789 },
  { productName: 'Lenovo Microwave 6', price: 15017 },
  { productName: 'Samsung Fiction 7', price: 70862 },
  { productName: 'LG Women 8', price: 43068 },
  { productName: 'HP iPhone 9', price: 74658 },
  { productName: 'OnePlus Beverages 10', price: 60053 },
  { productName: 'Sony Staples 11', price: 88370 },
  { productName: 'Dell Fitness 12', price: 39639 },
  { productName: 'Lenovo Camera 13', price: 48099 },
  { productName: 'Lenovo Football 14', price: 26405 },
  { productName: 'OnePlus Microwave 15', price: 36991 },
  { productName: 'LG Education 16', price: 38658 },
  { productName: 'OnePlus Men 17', price: 68684 },
  { productName: 'LG Staples 18', price: 35072 },
  { productName: 'Boat Smartwatch 19', price: 20772 },
  { productName: 'Apple Men 20', price: 58484 }
]


db.aggex.aggregate([
  {
    $project: {
      _id: 0,
      productName: 1,
      price: 1,
      quantity: 1,
      totalValue: {
        $multiply: ["$price", "$quantity"]
      }
    }
  }
])


  {
    productName: 'AmazonBasics Men 1',
    price: 60472,
    quantity: 5,
    totalValue: 302360
  },
  {
    productName: 'Samsung Business 2',
    price: 41620,
    quantity: 3,
    totalValue: 124860
  },
  {
    productName: 'Apple Fitness 3',
    price: 47754,
    quantity: 1,
    totalValue: 47754
  },
  {
    productName: 'LG Speaker 4',
    price: 46807,
    quantity: 2,
    totalValue: 93614
  },
  {
    productName: 'Lenovo Speaker 5',
    price: 61789,
    quantity: 3,
    totalValue: 185367
  },
  {
    productName: 'Lenovo Microwave 6',
    price: 15017,
    quantity: 5,
    totalValue: 75085
  },
  {
    productName: 'Samsung Fiction 7',
    price: 70862,
    quantity: 1,
    totalValue: 70862
  },
  {
    productName: 'LG Women 8',
    price: 43068,
    quantity: 5,
    totalValue: 215340
  },
  {
    productName: 'HP iPhone 9',
    price: 74658,
    quantity: 2,
    totalValue: 149316
  },
  {
    productName: 'OnePlus Beverages 10',
    price: 60053,
    quantity: 5,
    totalValue: 300265
  },
  {
    productName: 'Sony Staples 11',
    price: 88370,
    quantity: 2,
    totalValue: 176740
  },
  {
    productName: 'Dell Fitness 12',
    price: 39639,
    quantity: 5,
    totalValue: 198195
  },
  {
    productName: 'Lenovo Camera 13',
    price: 48099,
    quantity: 3,
    totalValue: 144297
  },
  {
    productName: 'Lenovo Football 14',
    price: 26405,
    quantity: 5,
    totalValue: 132025
  },
  {
    productName: 'OnePlus Microwave 15',
    price: 36991,
    quantity: 4,
    totalValue: 147964
  },
  {
    productName: 'LG Education 16',
    price: 38658,
    quantity: 3,
    totalValue: 115974
  },
  {
    productName: 'OnePlus Men 17',
    price: 68684,
    quantity: 1,
    totalValue: 68684
  },
  {
    productName: 'LG Staples 18',
    price: 35072,
    quantity: 3,
    totalValue: 105216
  },
  {
    productName: 'Boat Smartwatch 19',
    price: 20772,
    quantity: 1,
    totalValue: 20772
  },
  {
    productName: 'Apple Men 20',
    price: 58484,
    quantity: 3,
    totalValue: 175452
  }
]

db.aggex.aggregate([
  {
    $group: {
      _id: "$category"
    }
  }
])

  { _id: 'Sports' },
  { _id: 'Grocery' },
  { _id: 'Fashion' },
  { _id: 'Electronics' },
  { _id: 'Home Appliances' },
  { _id: 'Mobiles' },
  { _id: 'Furniture' },
  { _id: 'Books' },
  { _id: 'Beauty' },
  { _id: 'Laptops' }
]
