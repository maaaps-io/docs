# Maaaps API

Table of Contents
=================

1. [General information](#general-information)
   
   1.1. [URL](#url)
   
   1.2. [Version](#version)
   
   1.3. [Requests](#requests)
   
   1.4. [Responses](#responses)
   
   1.5. [Country codes](#country-codes)
   

2. [API Methods](#api-methods)
   
   2.1. [Direct geocoder](#direct-geocoder)

   2.2. [Reverse geocoder](#reverse-geocoder)

   2.3. [Suggestions](#suggestions)


3. [Response models](#response-models)

   3.1. [Address model](#address-model)

   3.2. [Direct geocoder model](#direct-geocoder-model)

   3.3. [Reverse geocoder model](#reverse-geocoder-model)

   3.4. [Suggestions model](#suggestions-model)

General information
===================

Maaaps API allows to receive coordinates for the transmitted address, receive detailed address information on coordinates and receive suggestions for a part of the transmitted address. Works in **WGS84 (4326 by EPSG)**.

URL
---
Our main API service is available here:

``https://api.maaaps.io``

If your infrastructure is located in Asia, we recommend using our servers in Singapore:

``https://sgp.api.maaaps.io``

Version
-------
The current version of the API is **1.0**.

Requests
--------

You need to use in HTTP requests only HTTPS protocol and UTF-8 encoding.
All requests require a header **X-Maaaps-Api-Token**.

Responses
---------

All responses are returned in JSON format and UTF-8 encoding.

Possible response HTTP status codes:
 1. **200 OK**. The request was processed successfully.
 2. **400 Bad Request**. The request contains invalid parameters.
 3. **401 Unauthorized**. Token is required for this request.
 4. **403 Forbidden**. Not enough token rights for this request.
 5. **404 Not Found**. Unknown API Method.
 6. **500 Internal Server Error**. The error is related to technical problems on the server.

Country codes
-------------

Available country codes:
 - **in** India
 - **id** Indonesia
 - **eg** Egypt
 - **ph** Philippines
 - **br** Brazil
 - **sa** Saudi Arabia
 - **vn** Vietnam
 - **tr** Turkey

API methods
===========

Direct geocoder
---------------

``GET /v1.0/geocoder/<country_code>/direct``

Direct geocoder allows to receive coordinates for the transmitted address.

Required parameters:
 - **address** String

Request example:
```bash
curl --header 'X-Maaaps-Api-Token: XXXXXXX' 'https://api.maaaps.io/v1.0/geocoder/in/direct?address=630 Ongpin Street Binondo Manila'
```

Response example:
```json
{
   "requested_address": "630 Ongpin Street Binondo Manila",
   "address": {
      "formatted_address": "Binondo Paco Fire Search and Rescue Brigade, 630, Ongpin Street, Binondo, Third District, Manila, Capital District, Metro Manila",
      "postcode": null,
      "region": "Metro Manila",
      "state": null,
      "state_district": "Capital District",
      "city": "Manila",
      "city_district": "Third District",
      "suburb": "Binondo",
      "quarter": null,
      "neighbourhood": null,
      "road": "Ongpin Street",
      "name": "Binondo Paco Fire Search and Rescue Brigade",
      "building_number": "630",
      "amenity": "fire_station",
      "source": "osm",
      "location": {
         "lat": "14.6002",
         "lon": "120.97524"
      },
      "max_straight_distance_meters": null
   },
   "accuracy_level": "building"
}
```

Reverse geocoder
----------------

``GET /v1.0/geocoder/<country_code>/reverse``

Geocoder allows to receive detailed address information on coordinates.

Required parameters, works in **WGS84 (4326 by EPSG)**:
- **lat** Float
- **lon** Float

Optional parameters:
- **radius_meters** Int, by default 100. Min - 100, Max - 1000
- **limit** Int, by default 1. Min - 1, Max - 100

Request example:
```bash
curl --header 'X-Maaaps-Api-Token: XXXXXXX' 'https://api.maaaps.io/v1.0/geocoder/ph/reverse?lat=14.6002&lon=120.97524&limit=2&radius_meters=100'
```

Response example:
```json
{
   "requested_lat": "14.6002",
   "requested_lon": "120.97524",
   "data": [
      {
         "address": {
            "formatted_address": "Binondo Paco Fire Search and Rescue Brigade, 630, Ongpin Street, Binondo, Third District, Manila, Capital District, Metro Manila",
            "postcode": null,
            "region": "Metro Manila",
            "state": null,
            "state_district": "Capital District",
            "city": "Manila",
            "city_district": "Third District",
            "suburb": "Binondo",
            "quarter": null,
            "neighbourhood": null,
            "road": "Ongpin Street",
            "name": "Binondo Paco Fire Search and Rescue Brigade",
            "building_number": "630",
            "amenity": "fire_station",
            "source": "osm",
            "location": {
               "lat": "14.6002",
               "lon": "120.97524"
            },
            "max_straight_distance_meters": null
         },
         "straight_distance_meters": 0
      },
      {
         "address": {
            "formatted_address": "TxtFire, 650, Ongpin Street, Binondo, Third District, Manila, Capital District, Metro Manila",
            "postcode": null,
            "region": "Metro Manila",
            "state": null,
            "state_district": "Capital District",
            "city": "Manila",
            "city_district": "Third District",
            "suburb": "Binondo",
            "quarter": null,
            "neighbourhood": null,
            "road": "Ongpin Street",
            "name": "TxtFire",
            "building_number": "650",
            "amenity": null,
            "source": "osm",
            "location": {
               "lat": "14.60011",
               "lon": "120.97523"
            },
            "max_straight_distance_meters": null
         },
         "straight_distance_meters": 10
      }
   ]
}
```

Suggestions
-----------

``GET /v1.0/geocoder/<country_code>/suggestions``

Geocoder allows to receive coordinates for the transmitted address.

Required parameters:
- **address** String

Request example:
```bash
curl --header 'X-Maaaps-Api-Token: XXXXXXX' 'https://api.maaaps.io/v1.0/geocoder/in/suggestions?address=Zone'
```

Response example (in this case we show only 2 suggested addresses):
```json
{
   "requested_address": "Ongpin Street",
   "addresses": [
      {
         "formatted_address": "Great Buddha Cafe, Binondo Manila0, Ongpin Street, Binondo, Third District, Manila, Capital District, Metro Manila",
         "postcode": null,
         "region": "Metro Manila",
         "state": null,
         "state_district": "Capital District",
         "city": "Manila",
         "city_district": "Third District",
         "suburb": "Binondo",
         "quarter": null,
         "neighbourhood": null,
         "road": "Ongpin Street",
         "name": "Great Buddha Cafe",
         "building_number": "Binondo Manila0",
         "amenity": "restaurant",
         "source": "osm",
         "location": {
            "lat": "14.600095",
            "lon": "120.975145"
         },
         "max_straight_distance_meters": null
      },
      {
         "formatted_address": "Nachang Cafe, Greater Lagro, 5th District, Quezon City, Eastern Manila District, Metro Manila, 1118",
         "postcode": "1118",
         "region": "Metro Manila",
         "state": null,
         "state_district": "Eastern Manila District",
         "city": "Quezon City",
         "city_district": "5th District",
         "suburb": null,
         "quarter": null,
         "neighbourhood": "Greater Lagro",
         "road": null,
         "name": "Nachang Cafe",
         "building_number": null,
         "amenity": "cafe",
         "source": "osm",
         "location": {
            "lat": "14.735108",
            "lon": "121.063708"
         },
         "max_straight_distance_meters": null
      }
   ]
}
```

Response models
===============

Address model
-------------

Model parameters:

**formatted_address** ``string``

The address string formed according to the format generally accepted for specific countries. Includes all fields from the response (from postcode to building_number).

**postcode** ``string, nullable``

The postcode (zipcode) of address.

**region** ``string, nullable``

Describes an administration area with no specific political signification. For example: Metro Manila (Philippines).

**state** ``string, nullable``

High-level sub-national political entity: province (Canada, Philippines), state (USA, Mexico).

**state_district** ``string, nullable``

The district of state. For example: Eastern Manila District of Metro Manila (Philippines).

**city** ``string, nullable``
  
The name of city (provincial capitals, major conurbations, towns). For example: Quezon City in Metro Manila (Philippines).

**city_district** ``string, nullable``
  
The district of city. For example: 5th District in Quezon City Metro Manila (Philippines).

**suburb** ``string, nullable``

The name of the populated area or locality located outside the administrative boundary of the city. For example: Bago Bantay Quezon City in Metro Manila (Philippines).

**quarter** ``string, nullable``

The part of a big settlement. Usually it's smaller than suburb. For example for this address "Barangay 116, Zone 10, Grace Park East, District 2, Caloocan, Northern Manila District, Metro Manila" Quarter is "Zone 10".

**neighbourhood** ``string, nullable``

A neighbourhood is a small named geographically localised place. Usually it's smaller than quarter. For example for this address "Barangay 116, Zone 10, Grace Park East, District 2, Caloocan, Northern Manila District, Metro Manila" neighbourhood is "Barangay 116".

**road** ``string, nullable``

Name of road, street, highway.

**name** ``string, nullable``

Name of building, school, cafe, etc.

**building_number** ``string, nullable``

Number of building. Can contain not only numeric values.

**source** ``string``

Source of data. Can contain values: ``osm`` - source of data is OSM, ``maaaps`` - source of data is Maaaps, ``approximation`` - point position has been calculated. 

**location** ``object``

Geo location of address. It's object with fields: **lat** ``string``, **lon** ``string``. Response in **WGS84 (4326 by EPSG)**.

**max_straight_distance_meters**

Sometimes the API cannot find a specific house. In this case, the response will contain data on the found smallest administrative division. The **location** will contain the centroid point of the administrative polygon. The **max_straight_distance_meters** will contain the distance in meters from the centroid to the farthest point of the administrative division polygon.


Direct geocoder model
---------------------

Model parameters:

**requested_address** ``string``

Address from request

**address** ``Address model, nullable``

See [Address model](#address-model)

**accuracy_level** ``string, nullable``

The level of accuracy of the found address. Can contain values: ``unknown``, ``postcode``, ``region``, ``state``, ``state_district``, ``city``, ``city_district``, ``suburb``, ``quarter``, ``neighbourhood``, ``road``, ``building``.


Reverse geocoder model
---------------------

Model parameters:

**requested_lat** ``string``

Latitude from request

**requested_lon** ``string``

Longitude from request

**data** ``Array``

Contains list of found addresses in ascending order from the requested location. Each list item contains fields: **address** (see [Address model](#address-model)) and **straight_distance_meters** (straight distance in meters from requested location to found address).


Suggestions model
---------------------

Model parameters:

**requested_address** ``string``

Address from request

**addresses** ``Address[]``

List of address models (see [Address model](#address-model)) in descending order of matching with the requested address.
