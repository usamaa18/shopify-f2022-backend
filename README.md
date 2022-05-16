#   

# References

Used [express-generator](https://expressjs.com/en/starter/generator.html)
Used [mongoose-id-validator](https://www.npmjs.com/package/mongoose-id-validator)
Used Shopify's logo as favicon.ico. No trademark infringement intended.

# APIs

Create item <code>POST /items</code>

Edit item <code>POST /items/{id}</code>

Delete item <code>DELETE /items/{id}</code>

List items <code>GET /items</code>

Create location <code>POST /locations</code>



# Database Schema

## Item

- ID
- Description
- Weight
- Length
- Width
- Height
- Location

## Warehouse

- ID
- Name -- String
- Location -- (GeoJSON)[https://mongoosejs.com/docs/geojson.html]