


# Database Schema

### Item

- ID
- desc
- weight
- length
- width
- height
- warehouseId -- (links to Warehouse)

### Warehouse

- ID
- name
- location -- (datatype: [GeoJSON](https://mongoosejs.com/docs/geojson.html))


# REST API

The REST API to the example app is described below.

## Get list of items

### Request

`GET /items`

    curl --location --request GET 'http://localhost:3000/v1/items'

### Response

    Status: 200 OK
    Content-Type: application/json

    [{item1}, {item2}, ...]


## Get list of items when no items in inventory

### Request

`GET /items`

    curl --location --request GET 'http://localhost:3000/v1/items'

### Response

    Status: 200 OK
    Content-Type: application/json

    []


## Create new item

### Request

`POST /items`

    curl --location --request POST 'http://localhost:3000/v1/items' \
        --header 'Content-Type: application/x-www-form-urlencoded' \
        --data-urlencode 'description=iPhone 13' \
        --data-urlencode 'weight=3.3' \
        --data-urlencode 'length=10' \
        --data-urlencode 'width=5' \
        --data-urlencode 'height=3' \
        --data-urlencode 'warehouseId=6281cff83d222c6c47382462'

### Response

    Status: 200 OK
    Content-Type: application/json

    {
    "desc": "iPhone 13",
    "weight": 3.3,
    "length": 10,
    "width": 5,
    "height": 3,
    "warehouseId": "6281cff83d222c6c47382462",
    "_id": "62826bf6b3f9087a71667a46",
    "__v": 0
    }


## Edit an item

### Request

`POST /items/{id}`

    curl --location --request POST 'http://localhost:3000/v1/items/62826bf6b3f9087a71667a46' \
        --header 'Content-Type: application/x-www-form-urlencoded' \
        --data-urlencode 'weight=20'

### Response

    Status: 200 OK
    Content-Type: application/json

    {
    "_id": "62826bf6b3f9087a71667a46",
    "desc": "iPhone 13",
    "weight": 20,
    "length": 10,
    "width": 5,
    "height": 3,
    "warehouseId": "6281cff83d222c6c47382462",
    "__v": 0
    }


## Delete an item

### Request

`DELETE /items/{id}`

    curl --location --request DELETE 'http://localhost:3000/v1/items/62826bf6b3f9087a71667a46'

### Response

    Status: 200 OK
    Content-Type: text/html

    Deleted item successfully


## Delete same item again

### Request

`DELETE /items/{id}`

    curl --location --request DELETE 'http://localhost:3000/v1/items/62826bf6b3f9087a71667a46'

### Response

    Status: 400 BAD REQUEST
    Content-Type: text/html

    Invalid item (itemId not found in DB)


## Edit deleted item

### Request

`POST /items/{id}`

    curl --location --request POST 'http://localhost:3000/v1/items/62826bf6b3f9087a71667a46' \
        --header 'Content-Type: application/x-www-form-urlencoded' \
        --data-urlencode 'weight=20'

### Response

    Status: 404 NOT FOUND
    Content-Type: text/html

    Invalid item (itemId not found in DB)


## Create new warehouse

### Request

`POST /warehouses`

    curl --location --request POST 'http://localhost:3000/v1/warehouses' \
        --header 'Content-Type: application/x-www-form-urlencoded' \
        --data-urlencode 'name=Montreal' \
        --data-urlencode 'longitude=73.5673' \
        --data-urlencode 'latitude=45.5017'

### Response

    Status: 200 OK
    Content-Type: application/json

    {
    "name": "Montreal",
    "location": {
        "type": "Point",
        "coordinates": [
            73.5673,
            45.5017
        ]
    },
    "_id": "62826ed0b3f9087a71667a50",
    "__v": 0
    }


# References

- Used [express-generator](https://expressjs.com/en/starter/generator.html).
- Used [mongoose-id-validator](https://www.npmjs.com/package/mongoose-id-validator).
- Used Shopify's logo as favicon.ico. No trademark infringement intended.