# Maaaps API

Table of Contents
=================

1. [General information](#general-information)
   
   1.1. [URL](#url)
   
   1.2. [Version](#version)
   
   1.3. [Requests](#requests)
   
   1.4. [Responses](#responses)
   
   1.5. [Country codes](#country-codes)
   
2. [Direct geocoder](#direct-geocoder)

3. [Reverse geocoder](#reverse-geocoder)

4. [Suggestions](#suggestions)

General information
===================

Maaaps API allows to receive coordinates for the transmitted address, receive detailed address information on coordinates and receive suggestions for a part of the transmitted address.

URL
---
Our main API service is available here:

``https://api.maaaps.io``

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

Direct geocoder
===============

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
      "formatted_address": "630 Ongpin Street Binondo Third District Manila Metro Manila Luzon",
      "postcode": null,
      "region": "Luzon",
      "city": "Manila Metro Manila",
      "state_district": null,
      "suburb": "Binondo",
      "city_district": "Third District",
      "quarter": null,
      "road": "Ongpin Street",
      "name": null,
      "building_number": "630",
      "amenity": "fire_station",
      "location": {
         "lat": 14.6002,
         "lon": 120.97524
      }
   },
   "accuracy_level": "building"
}
```

Reverse geocoder
================
``GET /v1.0/geocoder/<country_code>/reverse``

Geocoder allows to receive detailed address information on coordinates.

Required parameters:
- **lat** Float
- **lon** Float

Optional parameters:
- **radius_meters** Int, by default 100. Min - 100, Max - 1000
- **limit** Int, by default 1. Min - 1, Max - 100

Request example:
```bash
curl --header 'X-Maaaps-Api-Token: XXXXXXX' 'https://api.maaaps.io/v1.0/geocoder/in/reverse?lat=14.6002&lon=120.97524&limit=2'
```

Response example:
```json
{
   "requested_lat": "14.6002",
   "requested_lon": "120.97524",
   "data": [
      {
         "address": {
            "formatted_address": "630 Ongpin Street Binondo Third District Manila Metro Manila Luzon",
            "postcode": null,
            "region": "Luzon",
            "city": "Manila Metro Manila",
            "state_district": null,
            "suburb": "Binondo",
            "city_district": "Third District",
            "quarter": null,
            "road": "Ongpin Street",
            "name": null,
            "building_number": "630",
            "amenity": "fire_station",
            "location": {
               "lat": 14.6002,
               "lon": 120.97524
            }
         },
         "straight_distance_meters": 0
      },
      {
         "address": {
            "formatted_address": "650 Ongpin Street Binondo Third District Manila Metro Manila Luzon",
            "postcode": null,
            "region": "Luzon",
            "city": "Manila Metro Manila",
            "state_district": null,
            "suburb": "Binondo",
            "city_district": "Third District",
            "quarter": null,
            "road": "Ongpin Street",
            "name": null,
            "building_number": "650",
            "amenity": null,
            "location": {
               "lat": 14.60011,
               "lon": 120.97523
            }
         },
         "straight_distance_meters": 10
      }
   ]
}
```

Suggestions
===========

``GET /v1.0/geocoder/<country_code>/suggestions``

Geocoder allows to receive coordinates for the transmitted address.

Required parameters:
- **address** String

Request example:
```bash
curl --header 'X-Maaaps-Api-Token: XXXXXXX' 'https://api.maaaps.io/v1.0/geocoder/in/suggestions?address=Zone'
```

Response example:
```json
{
   "requested_address": "Ongpin Street",
   "addresses": [
      {
         "formatted_address": "Binondo Manila Ongpin Street Binondo Third District Manila Metro Manila Luzon",
         "postcode": null,
         "region": "Luzon",
         "city": "Manila Metro Manila",
         "state_district": null,
         "suburb": "Binondo",
         "city_district": "Third District",
         "quarter": null,
         "road": "Ongpin Street",
         "name": null,
         "building_number": "Binondo Manila",
         "amenity": "restaurant",
         "location": {
            "lat": 14.600095,
            "lon": 120.975145
         }
      },
      {
         "formatted_address": "630 Ongpin Street Binondo Third District Manila Metro Manila Luzon",
         "postcode": null,
         "region": "Luzon",
         "city": "Manila Metro Manila",
         "state_district": null,
         "suburb": "Binondo",
         "city_district": "Third District",
         "quarter": null,
         "road": "Ongpin Street",
         "name": null,
         "building_number": "630",
         "amenity": "fire_station",
         "location": {
            "lat": 14.6002,
            "lon": 120.97524
         }
      }
   ]
}
```
