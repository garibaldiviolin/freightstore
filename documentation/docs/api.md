# Maps endpoint

URL that allows the creation the map resources

- URL: `/api/v1/maps/`
- HTTP Method(s) Accepted: `POST`
- Format: `JSON`

**Body Params**

Field        | Type    | Required  | Description
------------ | ------- | --------- | ---------------
name         | string  | Yes       | The map's name

**Status Codes**

- HTTP Status Code

Type         | Status Code
------------ | -------------
Success      | 201 (Created)
Error        | 400 (Bad Request)

**Request example:**

```
{
    "name": "California"
}
```

**Response example:**

- HTTP Status Code: `201 (Created)`
- The same JSON body data of the request (above)

# Map Routes endpoint

URL that receives and creates all of the map routes (with the origin and destination point) from the client. The client must have already sent (register) a map_name in the endpoint above before sending the map-routes. This endpoint only accepts the HTTP POST method (resouce creation).

- URL: `/api/v1/maps-routes/`
- HTTP Method(s) Accepted: `POST`
- Format: `JSON`

**Body Params**

Field             | Type     | Required | Description
----------------- | -------- | -------- | -------------------------
freight_map       | string   | Yes      | It's the same information sent in the maps endpoint (map_name).
origin_point      | string   | Yes      | The point name where the route starts.
destination_point | string   | Yes      | The point name where the route ends. It must be different from the origin_point field.
distance          | float    | Yes      | The distance between origin and destination points (in kilometers)

**Status Codes**

- HTTP Status Code

Type         | Status Code
------------ | -------------
Success      | 201 (Created)
Error        | 400 (Bad Request)

**Error Messages**

Message                             | Reason
----------------------------------- | -------------------------------------------------------------
Distance must be greater than zero. | Distance field was sent with a value equal or less than zero.
Origin must be different from destination point.' | origin_point and destination_point was sent with the same value.

**Request example:**

HTTP Status Code: `201 (Created)`
```
{
    "freight_map": "California",
    "origin_point": "X",
    "destination_point": "Y",
    "distance": 81232.594
}
```

**Response example:**

```
{
    "freight_map": "California",
    "origin_point": "X",
    "destination_point": "Y",
    "distance": "81232.594"
}
```

# Shortest Path endpoint

URL that responds the shortest path and freight cost based on the map name, origin and destination points, fuel litter price and vehicle's fuel consumption, given in the URL.

- URL: `/api/v1/shortest-path/`
- HTTP Method(s) Accepted: `GET`
- Format: `JSON`

**URL Request Params**

Field             | Type    | Required  | Description
----------------- | ------- | --------- | ---------------
map_name          | string  | Yes       | The same information sent in the /api/v1/maps/ endpoint (map_name).
origin_point      | string  | Yes       | The freight's starting point. It must be one of the points given in the /api/v1/map-routes/ endpoint.
destination_point | string  | Yes       | The same information sent in the /api/v1/maps/ endpoint (map_name).
fuel_litter_price | float   | Yes       | The fuel litter price must be a integer or decimal number.
fuel_consumption  | float   | Yes       | The freight vehicle's fuel consumption (in kilometers per fuel litter). It must be a integer or decimal number.

**Body Response Format**

Field             | Type    | Required  | Description
----------------- | ------- | --------- | ---------------
shortest_path     | string  | Yes       | The map points sequence (routes) that represents the shortest path between the origin and the destination point given in the request
freight_rate      | string  | Yes       | The freight's calculated price

**Status Codes**

- HTTP Status Code

Type         | Status Code
------------ | -------------
Success      | 200 (OK)
Error        | 400 (Bad Request)

**Error Messages**

Message                             | Reason
----------------------------------- | -------------------------------------------------------------
map_name parameter must be supplied | The map_name URL parameter was not informed.
origin_point parameter must be supplied | The origin_point URL parameter was not informed.
destination_point parameter must be supplied | The destination_point URL parameter was not informed.
origin_point must be different from destination_point. | The origin_point and destination point informed in the URL are the same.
fuel_litter_price parameter must be supplied | The fuel_litter_price URL parameter was not informed.
fuel_litter_price must be numeric. | The fuel_litter_price was informed with an invalid format.
fuel_consumption parameter must be supplied | The fuel_consumption URL parameter was not informed.
fuel_consumption must be numeric.  | The fuel_consumption was informed with an invalid format.

**URL Request example:**
```
/api/v1/shortest-path/?map_name=California&origin_point=B&destination_point=Y&fuel_litter_price=2.985&fuel_consumption=11.912
```

**Response example:**

HTTP Status Code: `200 (OK)`
```
{
    "shortest_path": "['H', 'A', 'P']",
    "freight_rate": "982.13"
}
```
