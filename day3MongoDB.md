=========================================================
MONGODB AGGREGATION - aggex
QUERY AND OUTPUT REFERENCE
=========================================================


1 : $match

QUERY
-----

db.aggex.aggregate([
    {
        $match: {
            category: "Books"
        }
    }
]);

OUTPUT

[
  {
    _id: ObjectId('b1501e7d1b82b0e61d3b8b9c'),
    productId: 'PROD00001',
    productName: 'Adidas Programming 1',
    category: 'Books',
    subCategory: 'Programming',
    brand: 'Adidas',
    price: 27981,
    discountPercentage: 3,
    discountedPrice: 27142,
    quantity: 5,
    revenue: 135710,
    rating: 4,
    reviewCount: 1083,
    stock: 305,
    inStock: true,
    seller: {
      name: 'DigitalMart',
      sellerRating: 4.7
    },
    customer: {
      customerId: 'CUS0841',
      city: 'Pune',
      state: 'Telangana',
      age: 56
    },
    payment: {
      method: 'Credit Card',
      transactionId: 'TXNnixxg5pjvu'
    },
    orderStatus: 'Delivered',
    orderDate: ISODate('2025-09-09T21:41:12.854Z'),
    tags: [ 'trending', 'premium' ],
    specifications: {
      warranty: '3 years',
      color: 'Red',
      weight: 1.99
    },
    isFeatured: false,
    createdAt: ISODate('2026-09-16T08:11:06.761Z')
  },
  {
    _id: ObjectId('636b476ff15449082828614d'),
    productId: 'PROD00004',
    productName: 'Adidas Programming 4',
    category: 'Books',
    subCategory: 'Programming',
    brand: 'Adidas',
    price: 34074,
    discountPercentage: 46,
    discountedPrice: 18400,
    quantity: 3,
    revenue: 55200,
    rating: 2.5,
    reviewCount: 3944,
    stock: 121,
    inStock: true,
    seller: {
      name: 'SmartShop',
      sellerRating: 2
    },
    customer: {
      customerId: 'CUS0987',
      city: 'Delhi',
      state: 'Karnataka',
      age: 25
    },
    payment: {
      method: 'Cash on Delivery',
      transactionId: 'TXNivbiohh8xp'
    },
    orderStatus: 'Processing',
    orderDate: ISODate('2025-05-27T12:53:06.841Z'),
    tags: [ 'premium', 'discount' ],
    specifications: {
      warranty: '1 years',
      color: 'White',
      weight: 1.17
    },
    isFeatured: true,
    createdAt: ISODate('2026-09-16T08:11:06.761Z')
  }
]

Type "it" for more

Matched documents : 489


2 : $match with $gt

QUERY
-----

db.aggex.aggregate([
    {
        $match: {
            price: { $gt: 50000 }
        }
    }
]);

OUTPUT
------

[
  {
    _id: ObjectId('4a9c02e7bb1d5f3390ac71de'),
    productId: 'PROD00002',
    productName: 'Nike Staples 2',
    category: 'Grocery',
    subCategory: 'Staples',
    brand: 'Nike',
    price: 70917,
    discountPercentage: 18,
    discountedPrice: 58152,
    quantity: 1,
    revenue: 58152,
    rating: 3.6,
    reviewCount: 2417,
    stock: 268,
    inStock: true,
    seller: {
      name: 'RetailHub',
      sellerRating: 3.1
    },
    customer: {
      customerId: 'CUS0312',
      city: 'Mumbai',
      state: 'Kerala',
      age: 41
    },
    payment: {
      method: 'UPI',
      transactionId: 'TXN7kq2mzab4d'
    },
    orderStatus: 'Shipped',
    orderDate: ISODate('2024-11-18T04:22:51.302Z'),
    tags: [ 'new', 'budget' ],
    specifications: {
      warranty: '2 years',
      color: 'Black',
      weight: 3.42
    },
    isFeatured: false,
    createdAt: ISODate('2026-09-16T08:11:06.761Z')
  }
]

Type "it" for more

Matched documents : 2372



3 : $match with $lt


QUERY
-----

db.aggex.aggregate([
    {
        $match: {
            price: { $lt: 50000 }
        }
    }
]);

OUTPUT
------

[
  {
    _id: ObjectId('b1501e7d1b82b0e61d3b8b9c'),
    productId: 'PROD00001',
    productName: 'Adidas Programming 1',
    category: 'Books',
    subCategory: 'Programming',
    brand: 'Adidas',
    price: 27981,
    discountPercentage: 3,
    discountedPrice: 27142,
    quantity: 5,
    revenue: 135710,
    rating: 4,
    reviewCount: 1083,
    stock: 305,
    inStock: true,
    seller: {
      name: 'DigitalMart',
      sellerRating: 4.7
    },
    customer: {
      customerId: 'CUS0841',
      city: 'Pune',
      state: 'Telangana',
      age: 56
    },
    payment: {
      method: 'Credit Card',
      transactionId: 'TXNnixxg5pjvu'
    },
    orderStatus: 'Delivered',
    orderDate: ISODate('2025-09-09T21:41:12.854Z'),
    tags: [ 'trending', 'premium' ],
    specifications: {
      warranty: '3 years',
      color: 'Red',
      weight: 1.99
    },
    isFeatured: false,
    createdAt: ISODate('2026-09-16T08:11:06.761Z')
  }
]

Type "it" for more

Matched documents : 2628


=========================================================
Q4 : $project
=========================================================

QUERY
-----

db.aggex.aggregate([
    {
        $project: {
            _id: 0,
            productName: 1,
            price: 1
        }
    }
]);

OUTPUT
------

[
  { productName: 'Adidas Programming 1', price: 27981 },
  { productName: 'Nike Staples 2',       price: 70917 },
  { productName: 'Nike Kids 3',          price: 50045 },
  { productName: 'Adidas Programming 4', price: 34074 }
]

Type "it" for more

Returned documents : 5000


=========================================================
Q5 : $project with $multiply
=========================================================

QUERY
-----

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
]);

OUTPUT
------

[
  {
    productName: 'Adidas Programming 1',
    price: 27981,
    quantity: 5,
    totalValue: 139905
  },
  {
    productName: 'Nike Staples 2',
    price: 70917,
    quantity: 1,
    totalValue: 70917
  },
  {
    productName: 'Nike Kids 3',
    price: 50045,
    quantity: 2,
    totalValue: 100090
  },
  {
    productName: 'Adidas Programming 4',
    price: 34074,
    quantity: 3,
    totalValue: 102222
  }
]

Type "it" for more

Returned documents : 5000


=========================================================
6 : $group
=========================================================

QUERY
-----

db.aggex.aggregate([
    {
        $group: {
            _id: "$category"
        }
    }
]);

OUTPUT
------

[
  { _id: 'Books' },
  { _id: 'Grocery' },
  { _id: 'Fashion' },
  { _id: 'Sports' },
  { _id: 'Furniture' },
  { _id: 'Beauty' },
  { _id: 'Mobiles' },
  { _id: 'Electronics' },
  { _id: 'Laptops' },
  { _id: 'Home Appliances' }
]

Returned documents : 10


=========================================================
Q7 : $match + $project
=========================================================

QUERY
-----

db.aggex.aggregate([
    {
        $match: {
            category: "Books"
        }
    },
    {
        $project: {
            _id: 0,
            productName: 1,
            price: 1
        }
    }
]);

OUTPUT
------

[
  { productName: 'Adidas Programming 1',  price: 27981 },
  { productName: 'Adidas Programming 4',  price: 34074 },
  { productName: 'OnePlus Programming 5', price: 48918 },
  { productName: 'Sony Programming 6',    price: 91151 }
]
