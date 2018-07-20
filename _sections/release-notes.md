---
title: Release notes
icon: fa-th
order: 3
---

# Release Notes

Changes:
---

#### Changed prices to have 2 decimals precision

Since: Jul 18th, 2018

Note: <span style="color:red">**breaking change**</span>

Request body should now contain a price element with 2 a decimal precision.  All currency elements in the response bodies now have a 2 decimal precision. Look below for more details.

New situation:

| Price           | Result        |
|:---------------:|:-------------:|
| 10.00           | Accepted      |
| 10.0            | Denied        |
| 10.000          | Denied        |

Old situation:

| Price           | Result        |
|:---------------:|:-------------:|
| 10.00           | Accepted      |
| 10.0            | Accepted      |
| 10.000          | Accepted      |

##### PUT Upsert Offer:

Description:
Validation checks have been added to the POST Upsert Offer endpoint to restrict the price element. You must provide a price with 2 decimals.

Example new request:
```$json
{
  "retailerOffer": [
    {
     "ean": "9789076174082",
      "condition": "NEW",
      "price": 10.00,
      "deliveryCode": "24uurs-21",
      "quantityInStock": 1,
      "publish": true,
      "referenceCode": "HarryPotter-nieuw",
      "fulfilmentMethod": "FBR"
    },
    {
      "ean": "9789076174082",
      "condition": "GOOD",
      "price": 7.50,
      "deliveryCode": "3-5d",
      "quantityInStock": 1,
      "publish": true,
      "referenceCode": "HarryPotter-2ehands",
      "description": "boek met een paar ezelsoren",
      "fulfilmentMethod": "FBR"
    },
    {
      "ean": "9789076174082",
      "condition": "REASONABLE",
      "price": 5.52,
      "deliveryCode": "3-5d",
      "quantityInStock": 1,
      "publish": true,
      "referenceCode": "HarryPotter-2ehands",
      "description": "boek met koffievlekken",
      "fulfilmentMethod": "FBR"
    }
  ]
}
```

Example old response:
```$json
{
  "retailerOffer": [
    {
     "ean": "9789076174082",
      "condition": "NEW",
      "price": 10,
      "deliveryCode": "24uurs-21",
      "quantityInStock": 1,
      "publish": true,
      "referenceCode": "HarryPotter-nieuw",
      "fulfilmentMethod": "FBR"
    },
    {
      "ean": "9789076174082",
      "condition": "GOOD",
      "price": 7.5,
      "deliveryCode": "3-5d",
      "quantityInStock": 1,
      "publish": true,
      "referenceCode": "HarryPotter-2ehands",
      "description": "boek met een paar ezelsoren",
      "fulfilmentMethod": "FBR"
    },
    {
      "ean": "9789076174082",
      "condition": "REASONABLE",
      "price": 5.523,
      "deliveryCode": "3-5d",
      "quantityInStock": 1,
      "publish": true,
      "referenceCode": "HarryPotter-2ehands",
      "description": "boek met koffievlekken",
      "fulfilmentMethod": "FBR"
    }
  ]
}
```

##### POST Bulk Commission:

Description:
Validation checks have been added to the POST Bulk commission endpoint to restrict the price element. You must provide a price with 2 decimals.

Example new request:
```$json
{
  "commissionQueries": [
    {
      "ean": "9789076174082",
      "condition": "NEW",
      "price": 10.00
    },
    {
      "ean": "9789076174082",
      "condition": "GOOD",
      "price": 7.50
    },
    {
      "ean": "9789076174082",
      "condition": "REASONABLE",
      "price": 5.52
    }
  ]
}
```

Example old request:
```$json
{
  "commissionQueries": [
    {
      "ean": "9789076174082",
      "condition": "NEW",
      "price": 10
    },
    {
      "ean": "9789076174082",
      "condition": "GOOD",
      "price": 7.5
    },
    {
      "ean": "9789076174082",
      "condition": "REASONABLE",
      "price": 5.523
    }
  ]
}
```


##### Endpoints with price elements in the response bodies

All response bodies with price elements, **except for invoice endpoints**, will now return two decimal precisions:

- GET   orders
- GET   single order
- GET   shipments
- GET   single shipment
- POST  bulk commission
- GET   single commission
- GET   single offer
- GET   purchasable shipping-labels

Description:
Added logic to transform any price to have a 2 decimal precision.

New situation:

| New response  |Old response   |
|:-------------:|:-------------:|
| **10.00**     | 10.00         |
| **10.00**     | 10.0          |
| **10.00**     | 10.000        |


Example new response:
```$json
{
    "orders": [
        {
            "orderId": “4123456789",
            "dateTimeOrderPlaced": "2018-07-18T14:13:31+02:00",
            "customerDetails": {
                "shipmentDetails": {
                    "salutationCode": “02",
                    "firstName": “Billie",
                    "surName": “Van der Bol.com",
                    "streetName": “Dorpstraat",
                    "houseNumber": “1",
                    "houseNumberExtended": "B",
                    "zipCode": “1111 ZZ",
                    "city": "Utrecht",
                    "countryCode": "NL",
                    "email": "2awq74td4z4mizmx6dcdbsdbdcna@verkopen.bol.com",
                    “company”: “bol.com"
                },
                "billingDetails": {
                    "salutationCode": “02",
                    "firstName": “Billie",
                    "surName": “Van der Bol.com",
                    "streetName": “Dorpstraat",
                    "houseNumber": “1",
                    "houseNumberExtended": "B",
                    "zipCode": “1111 ZZ",
                    "city": "Utrecht",
                    "countryCode": "NL",
                    "email": "2awq74td4z4mizmx6dcdbsdbdcna@verkopen.bol.com",
                    “company”: “bol.com"
                }
            },
            "orderItems": [
                {
                    "orderItemId": "2012345677",
                    "offerReference": “HarryPotter-nieuw ",
                    "ean": "9789076174082",
                    "quantity": 1,
                    "offerPrice": 10.00,
                    "transactionFee": 0.99,
                    "latestDeliveryDate": “2018-07-19",
                    "offerCondition": "NEW",
                    "cancelRequest": false,
                    "fulfilmentMethod": "FBR"
                },
		        {
                    "orderItemId": "2012345678",
                    "offerReference": “HarryPotter-2ehands",
                    "ean": "9789076174082",
                    “description”: "boek met een paar ezelsoren”,
                    "quantity": 1,
                    "offerPrice": 7.50,
                    "transactionFee": 0.99,
                    "latestDeliveryDate": "2018-07-23",
                    "offerCondition": "NEW",
                    "cancelRequest": false,
                    "fulfilmentMethod": "FBR"
                },
		        {
                    "orderItemId": "2012345679",
                    "offerReference": "HarryPotter-2ehands",
                    "ean": "9789076174082",
                    “description”: "boek met koffievlekken”,
                    "quantity": 1,
                    "offerPrice": 5.52,
                    "transactionFee": 0.99,
                    "latestDeliveryDate": "2018-07-23",
                    "offerCondition": "NEW",
                    "cancelRequest": false,
                    "fulfilmentMethod": "FBR"
                }
            ]
        }
    ]
}
```

Example old response:
```$json
{
    "orders": [
        {
            "orderId": “4123456789",
            "dateTimeOrderPlaced": "2018-07-18T14:13:31+02:00",
            "customerDetails": {
                "shipmentDetails": {
                    "salutationCode": “02",
                    "firstName": “Billie",
                    "surName": “Van der Bol.com",
                    "streetName": “Dorpstraat",
                    "houseNumber": “1",
                    "houseNumberExtended": "B",
                    "zipCode": “1111 ZZ",
                    "city": "Utrecht",
                    "countryCode": "NL",
                    "email": "2awq74td4z4mizmx6dcdbsdbdcna@verkopen.bol.com",
                    “company”: “bol.com"
                },
                "billingDetails": {
                    "salutationCode": “02",
                    "firstName": “Billie",
                    "surName": “Van der Bol.com",
                    "streetName": “Dorpstraat",
                    "houseNumber": “1",
                    "houseNumberExtended": "B",
                    "zipCode": “1111 ZZ",
                    "city": "Utrecht",
                    "countryCode": "NL",
                    "email": "2awq74td4z4mizmx6dcdbsdbdcna@verkopen.bol.com",
                    “company”: “bol.com"
                }
            },
            "orderItems": [
                {
                    "orderItemId": "2012345677",
                    "offerReference": “HarryPotter-nieuw ",
                    "ean": "9789076174082",
                    "quantity": 1,
                    "offerPrice": 10,
                    "transactionFee": 0.99,
                    "latestDeliveryDate": “2018-07-19",
                    "offerCondition": "NEW",
                    "cancelRequest": false,
                    "fulfilmentMethod": "FBR"
                },
		        {
                    "orderItemId": "2012345678",
                    "offerReference": “HarryPotter-2ehands",
                    "ean": "9789076174082",
                    “description”: "boek met een paar ezelsoren”,
                    "quantity": 1,
                    "offerPrice": 7.5,
                    "transactionFee": 0.99,
                    "latestDeliveryDate": "2018-07-23",
                    "offerCondition": "NEW",
                    "cancelRequest": false,
                    "fulfilmentMethod": "FBR"
                },
		        {
                    "orderItemId": "2012345679",
                    "offerReference": "HarryPotter-2ehands",
                    "ean": "9789076174082",
                    “description”: "boek met koffievlekken”,
                    "quantity": 1,
                    "offerPrice": 5.52,
                    "transactionFee": 0.99,
                    "latestDeliveryDate": "2018-07-23",
                    "offerCondition": "NEW",
                    "cancelRequest": false,
                    "fulfilmentMethod": "FBR"
                }
            ]
        }
    ]
}
```


#### Removed sellerId from Get Process Status response message 

Since: Jul 11th, 2018

Note: <span style="color:red">**breaking change**</span>

Process status:
 
All places where a process status is returned.

Description:
The response message from process status contained the sellerId this has been removed.

Example new response:
```$json
{  
   "processStatuses":[  
      {  
         "createTimestamp":"2018-11-14T09:34:41.000+01:00",
         "description":"Example request for processing 987654321.",
         "entityId":987654321,
         "errorMessage":"The example has been processed.",
         "eventType":"PROCESS_EXAMPLE",
         "id":1234567,
         "links":[  
            {  
               "href":"https://api.bol.com/retailer/process-status/v2/1234567",
               "method":"GET",
               "rel":"self"
            }
         ],
         "status":"SUCCESS"
      }
   ]
}
```

Example old response:
```$json
{  
   "processStatuses":[  
      {  
         "createTimestamp":"2018-11-14T09:34:41.000+01:00",
         "description":"Example request for processing 987654321.",
         "entityId":987654321,
         "errorMessage":"The example has been processed.",
         "eventType":"PROCESS_EXAMPLE",
         "id":1234567,
         "links":[  
            {  
               "href":"https://api.bol.com/retailer/process-status/v2/1234567",
               "method":"GET",
               "rel":"self"
            }
         ],
         "sellerId": 123456789,
         "status":"SUCCESS"
      }
   ]
}
```


#### New API call `Gets the status of an asynchronous process by entity id and event type for a seller` 

Since: Jun 5th, 2018

Process status:
 
GET /retailer/process-status

Description:
Retrieve a list of process statuses, which shows information regarding previously executed PUT/POST requests in descending order. You need to supply an entity id and event type.

#### Bug fix `return a 404 when no shipment is found instead of 500` 

Since: Jun 5th, 2018

Shipments:

GET /retailer/process-status/{shipment-id}

Description:
When we cannot find a shipment we now return a 404 Not Found.

---
#### Response for `Get an order by order id` gives back an order instead of giving back an array of orders.

Since: May 15th, 2018

Note: <span style="color:red">**breaking change**</span>

Example new response:
```$json
{
  "customerDetails": {
    "addressSupplement": "Lorem Ipsum",
    "city": "Utrecht",
    "company": "bol.com",
    "countryCode": "NL",
    "deliveryPhoneNumber": "012123456",
    "email": "billie@verkopen.bol.com",
    "extraAddressInformation": "Apartment",
    "firstName": "Billie",
    "houseNumber": 1,
    "houseNumberExtended": "B",
    "salutationCode": "02",
    "streetName": "Dorpstraat",
    "surname": "Jansen",
    "vatNumber": "NL999999999B99",
    "zipCode": "1111 ZZ"
  },
  "dateTimeOrderPlaced": "2017-02-09T12:39:48+01:00",
  "orderId": 4123456789,
  "orderItems": [
    {
      "cancelRequest": false,
      "ean": "0000007740404",
      "fulfilmentMethod": "FBR",
      "latestDeliveryDate": "2017-02-10",
      "offerCondition": "NEW",
      "offerPrice": 27.95,
      "offerReference": "BOLCOM00123",
      "orderItemId": 2012345678,
      "quantity": 10,
      "selectedDeliveryWindow": {
        "date": "2018-05-15T13:19:07Z",
        "end": "2018-05-15T13:19:07Z",
        "start": "2018-05-15T13:19:07Z"
      },
      "title": "Product Title",
      "transactionFee": 5.18
    }
  ]
}
```



Example old response:
```$json
{
  "orders": [
    {
      "customerDetails": {
        "addressSupplement": "Lorem Ipsum",
        "city": "Utrecht",
        "company": "bol.com",
        "countryCode": "NL",
        "deliveryPhoneNumber": "012123456",
        "email": "billie@verkopen.bol.com",
        "extraAddressInformation": "Apartment",
        "firstName": "Billie",
        "houseNumber": 1,
        "houseNumberExtended": "B",
        "salutationCode": "02",
        "streetName": "Dorpstraat",
        "surname": "Jansen",
        "vatNumber": "NL999999999B99",
        "zipCode": "1111 ZZ"
      },
      "dateTimeOrderPlaced": "2017-02-09T12:39:48+01:00",
      "orderId": 4123456789,
      "orderItems": [
        {
          "cancelRequest": false,
          "ean": "0000007740404",
          "fulfilmentMethod": "FBR",
          "latestDeliveryDate": "2017-02-10",
          "offerCondition": "NEW",
          "offerPrice": 27.95,
          "offerReference": "BOLCOM00123",
          "orderItemId": 2012345678,
          "quantity": 10,
          "selectedDeliveryWindow": {
            "date": "2018-05-15T13:19:07Z",
            "end": "2018-05-15T13:19:07Z",
            "start": "2018-05-15T13:19:07Z"
          },
          "title": "Product Title",
          "transactionFee": 5.18
        }
      ]
    }
  ]
}
```



