---
title: Grofers's API

language_tabs:
  - json

search: true
---

# Introduction

Welcome to the Grofers API! You can use our API to access Grofers API endpoints, which can get information on delivery and orders in our database.

For now we don't have lagunage bindings but we invite you to contribute in whatever language you write and share with the world! You can view code examples in the dark area to the right.

# Authentication

HTTP Basic Auth with username & password provided.




# Base URL

## Testing

### HTTP Request

`GET http://www.grofers.it:8080/rest/`

## Production

### HTTP Request

`GET http://www.grofers.com:8080/rest/`

# Place a new delivery order

POST /orders/

Content-type : application/json

## Post data

### Mandatory Keys:

Parameter | Description
--------- | -----------
merchantID | The ID of the merchant
pickupAddress & deliveryAddress |This field further contains the following fields:
                                |addressLine1 : The address for delivery and pickup
                                |addressLine2 : The address for delivery and pickup
                                |postCode : The post code of the area
                                |city : possible values "DELHI", "MUMBAI", "GURGAON", "NOIDA", "GHAZIABAD", "BANGALORE"
                                |gpsCoords : This could be either null or "latitude": 28.4878862, "longitude": 77.0644087

###Optional fields:

Parameter | Description
--------- | -----------
merchantOrderID | Order id generated/maintained on merchant side
scheduledTime | The time scheduled for delivery or pickup
collectableAmount | The amount to be collected

```json
{
  "merchantOrderID": "139968",
  "addComments": "Customer name, customer phone and other details you want to pass on to Grofers",
  "merchantID": "merchant-id",
  "pickupAddress": {
    "addressLine1": "Super  Trading & Marketing Private Limited, Plot no - 586",
    "addressLine2": "Ground Floor , Sector - 18",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null,
  },
  "deliveryAddress": {
    "addressLine1": "Gurgaon",
    "addressLine2": "",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "scheduledTime": 1417792450,
  "collectableAmount": 314,
}
```

## Response

On creating a new delivery order, you will receive a unique order-id

```json
{
  "orderID": "merchant-id-16",
  "merchantOrderID": "139968",
  "addComments": "Customer name, customer phone and other details you want to pass on to Grofers",
  "merchantID": "merchant-id",
  "pickupAddress": {
    "addressLine1": "Super  Trading & Marketing Private Limited, Plot no - 586",
    "addressLine2": "Ground Floor , Sector - 18",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "deliveryAddress": {
    "addressLine1": "Gurgaon",
    "addressLine2": "",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "delivererID": null,
  "status": "RECEIVED",
  "actionNotificationPreference": null,
  "orderActions": [
    {
      "action": "received",
      "time": 1417762789,
      "addOpts": null
    }
  ],
  "settlement": null,
  "scheduledTime": 0,
  "comments": null,
  "collectableAmount": 100,
  "podImage": null,
  "podLocation": null,
  "customerPhone": "9818511886",
  "orderImage": null
}
```

# Get details of an order

GET /orders/&lt;order_id&gt;

Where &lt;order_id&gt; is Grofers order id, eg : testorder-1

### List of possible order statuses: 

Status | Description
--------- | -----------
RECEIVED | Order has been received by Grofers
ASSIGNED | Order has been assigned to a field executive
ENROUTE | Field executive has picked the package from the pickup location
DELIVERED | Field executive has delivered to the delivery location
CANCELLED | Order has been Cancelled
UNSCHEDULED | Order has been received but not scheduled for delivery
RETURNED | Orders has been returned to merchant
ON_HOLD | Order is on hold

## Responses

<h3 class="content">Order status : RECEIVED</h3>

```json
{
  "orderID": "merchant-order-id",
  "merchantOrderID": "merchant-order-id",
  "addComments": "Customer name, customer phone and other details you want to pass on to Grofers",
  "merchantID": "merchant-id",
  "pickupAddress": {
    "addressLine1": "Super  Trading & Marketing Private Limited, Plot no - 586",
    "addressLine2": "Ground Floor , Sector - 18",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "deliveryAddress": {
    "addressLine1": "Gurgaon",
    "addressLine2": "",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "delivererID": null,
  "status": "RECEIVED",
  "actionNotificationPreference": null,
  "orderActions": [
    {
      "action": "received",
      "time": 1417762789,
      "addOpts": null
    }
  ],
  "settlement": null,
  "scheduledTime": 0,
  "comments": null,
  "collectableAmount": 100,
  "podImage": null,
  "podLocation": null,
  "customerPhone": "9818511886",
  "orderImage": null
}
```

<h3 class="content">Order status : ASSIGNED</h3>

```json
{
  "orderID": "merchant-order-id",
  "merchantOrderID": "merchant-order-id",
  "addComments": "Customer name, customer phone and other details you want to pass on to Grofers",
  "merchantID": "merchant-id",
  "pickupAddress": {
    "addressLine1": "Super Trading & Marketing Private Limited, Plot no - 586",
    "addressLine2": "Ground Floor , Sector - 18",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "deliveryAddress": {
    "addressLine1": "Gurgaon",
    "addressLine2": "",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "delivererID": "emp231",
  "status": "ASSIGNED",
  "actionNotificationPreference": null,
  "orderActions": [
    {
      "action": "received",
      "time": 1417762789,
      "addOpts": null
    },
    {
      "action": "assign",
      "time": 1417773747,
      "addOpts": "emp231"
    }
  ],
  "settlement": null,
  "scheduledTime": 0,
  "comments": null,
  "collectableAmount": 100,
  "podImage": null,
  "podLocation": null,
  "customerPhone": "9818511886",
  "orderImage": null
}
```

<h3 class="content">Order status : ENROUTE</h3>

```json
{
  "orderID": "merchant-order-id",
  "merchantOrderID": "merchant-order-id",
  "addComments": "Customer name, customer phone and other details you want to pass on to Grofers",
  "merchantID": "merchant-id",
  "pickupAddress": {
    "addressLine1": "Super Trading & Marketing Private Limited, Plot no - 586",
    "addressLine2": "Ground Floor , Sector - 18",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "deliveryAddress": {
    "addressLine1": "Gurgaon",
    "addressLine2": "",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "delivererID": "emp231",
  "status": "ENROUTE",
  "actionNotificationPreference": null,
  "orderActions": [
    {
      "action": "received",
      "time": 1417762789,
      "addOpts": null
    },
    {
      "action": "assign",
      "time": 1417773747,
      "addOpts": "emp231"
    },
    {
      "action": "picked",
      "time": 1417773872,
      "addOpts": null
    }
  ],
  "settlement": null,
  "scheduledTime": 0,
  "comments": null,
  "collectableAmount": 9010,
  "podImage": null,
  "podLocation": null,
  "customerPhone": "9818511886",
  "orderImage": null
}
```

<h3 class="content">STATUS: DELIVERED</h3>

```json
{
  "orderID": "merchant-order-id",
  "merchantOrderID": "merchant-order-id",
  "addComments": "Customer name, customer phone and other details you want to pass on to Grofers",
  "merchantID": "merchant-id",
  "pickupAddress": {
    "addressLine1": "Super Trading & Marketing Private Limited, Plot no - 586",
    "addressLine2": "First Floor , Sector - 18, Gurgaon",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "deliveryAddress": {
    "addressLine1": "Gurgaon",
    "addressLine2": "",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "delivererID": "emp231",
  "status": "DELIVERED",
  "actionNotificationPreference": null,
  "orderActions": [
    {
      "action": "received",
      "time": 1417762789,
      "addOpts": null
    },
    {
      "action": "assign",
      "time": 1417773747,
      "addOpts": "emp231"
    },
    {
      "action": "picked",
      "time": 1417773872,
      "addOpts": null
    },
    {
      "action": "delivered",
      "time": 1417773925,
      "addOpts": null
    }
  ],
  "settlement": null,
  "scheduledTime": 0,
  "comments": null,
  "collectableAmount": 100,
  "podImage": null,
  "podLocation": null,
  "customerPhone": "9999999999",
  "orderImage": null
}
```

<h3 class="content">STATUS : CANCELLED</h3>

```json
{
  "orderID": "merchant-order-id",
  "merchantOrderID": "merchant-order-id",
  "addComments": "Customer name, customer phone and other details you want to pass on to Grofers",
  "merchantID": "merchant-id",
  "pickupAddress": {
    "addressLine1": "Super Trading & Marketing Private Limited, Plot no - 586",
    "addressLine2": "First Floor , Sector - 18, Gurgaon",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "deliveryAddress": {
    "addressLine1": "Gurgaon",
    "addressLine2": "",
    "postCode": "122016",
    "city": "GURGAON",
    "gpsCoords": null
  },
  "delivererID": "emp231",
  "status": "CANCELLED",
  "actionNotificationPreference": null,
  "orderActions": [
    {
      "action": "received",
      "time": 1417762789,
      "addOpts": null
    },
    {
      "action": "cancelled",
      "time": 1417773747,
      "addOpts": "emp231"
    }
  ],
  "settlement": null,
  "scheduledTime": 0,
  "comments": null,
  "collectableAmount": 100,
  "podImage": null,
  "podLocation": null,
  "customerPhone": "9999999999",
  "orderImage": null
}
```

# Get All Orders

GET /orders/

## Response

```json
[
  {
    "orderID": "grmc210-23",
    "merchantOrderID": "",
    "addComments": "",
    "merchantID": "grmc210",
    "pickupAddress": {
      "addressLine1": "ads",
      "addressLine2": null,
      "postCode": "122015",
      "city": "GURGAON",
      "gpsCoords": null
    },
    "deliveryAddress": {
      "addressLine1": "",
      "addressLine2": null,
      "postCode": "",
      "city": null,
      "gpsCoords": null
    },
    "delivererID": null,
    "status": "RECEIVED",
    "actionNotificationPreference": null,
    "orderActions": [
      {
        "action": "received",
        "time": 1417792450,
        "addOpts": null
      }
    ],
    "settlement": null,
    "scheduledTime": 1417792440,
    "comments": null,
    "collectableAmount": 0,
    "podImage": null,
    "podLocation": null,
    "customerPhone": null,
    "orderImage": null
  },
  {
    "orderID": "grmc210-22",
    "merchantOrderID": "",
    "addComments": "sjdnkjsandkdn",
    "merchantID": "grmc210",
    "pickupAddress": {
      "addressLine1": "54B, first floor , sector 18",
      "addressLine2": null,
      "postCode": "122015",
      "city": "GURGAON",
      "gpsCoords": null
    },
    "deliveryAddress": {
      "addressLine1": "703, Essel towers",
      "addressLine2": null,
      "postCode": "",
      "city": "GURGAON",
      "gpsCoords": null
    },
    "delivererID": "emp231",
    "status": "ENROUTE",
    "actionNotificationPreference": null,
    "orderActions": [
      {
        "action": "received",
        "time": 1417679054,
        "addOpts": null
      },
      {
        "action": "assign",
        "time": 1417679069,
        "addOpts": "emp231"
      },
      {
        "action": "picked",
        "time": 1417679144,
        "addOpts": null
      }
    ],
    "settlement": null,
    "scheduledTime": 1417678980,
    "comments": null,
    "collectableAmount": 1000,
    "podImage": null,
    "podLocation": null,
    "customerPhone": null,
    "orderImage": null
  }
]
```
# Note

<aside class="notice">
You can view your delivery order by logging on [grofer.it] ( testing ) with credentials provided.
</aside>

<aside class="notice">
Need API access - Drop us an email at **sales@grofers.com**
</aside>

<style type="text/css">
h3{
clear: both;
border-bottom: 1px solid #ddd;
line-height: 2em;
}

 pre{
position: relative;
top: -10px;
}

.tocify-wrapper .tocify-focus{
background-color: #e96125;
}
</style>