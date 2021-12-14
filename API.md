# Maaaps API

Table of Contents
=================

1. [General information](#general-information)
   
   1.1. [URL](#url)
   
   1.2. [Version](#version)
   
   1.3. [Requests](#requests)
   
   1.4. [Responses](#responses)
   
   1.5. [Country codes](#country-codes)
   
2. [Geocoder](#geocoder)

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

Geocoder
========

``GET /v1.0/geocoder/<country_code>/location``

Geocoder allows to receive coordinates for the transmitted address.

Required parameters:
 - **address** String

Request example:
```bash
curl --header 'X-Maaaps-Api-Token: XXXXXXX' 'https://api.maaaps.io/v1.0/geocoder/in/location?address=Mumbai'
```

Response example:
```json
{
  "requested_address": "Mumbai",
  "point": {
    "formatted_address": "Mumbai, Mumbai Metropolitan Region, Mumbai Suburban, Maharashtra, India",
    "lat": "19.0759899",
    "lon": "72.8773928"
  }
}
```

Reverse geocoder
================
``GET /v1.0/geocoder/<country_code>/address``

Geocoder allows to receive detailed address information on coordinates.

Required parameters:
- **lat** Float
- **lon** Float

Request example:
```bash
curl --header 'X-Maaaps-Api-Token: XXXXXXX' 'https://api.maaaps.io/v1.0/geocoder/in/address?lat=19.180674&lon=72.8331'
```

Response example:
```json
{
  "requested_lat": "19.180674",
  "requested_lon": "72.8331",
  "accuracy_type": "city_district",
  "address_details": {
    "suburb": "Malad West",
    "city_district": "Zone 4",
    "city": "Mumbai",
    "municipality": "Mumbai Metropolitan Region",
    "state_district": "Mumbai Suburban",
    "state": "Maharashtra",
    "postcode": "400064",
    "country": "India",
    "country_code": "in"
  },
  "point": {
    "formatted_address": "Malad West, P/N Ward, Zone 4, Mumbai, Mumbai Metropolitan Region, Mumbai Suburban, Maharashtra, 400064, India",
    "lat": "19.180621360807",
    "lon": "72.833002036865"
  }
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
  "requested_address": "Zone",
  "suggestions": [
    {
      "address": "Zone 7 Ambattur, Ambattur, Thiruvallur District, Tamil Nadu, India"
    },
    {
      "address": "Zone 11 Valasaravakkam, Ambattur, Thiruvallur District, Tamil Nadu, India"
    },
    {
      "address": "East Zone, Bengaluru, Bangalore North, Bangalore Urban, Karnataka, India"
    },
    {
      "address": "Zone 3 Madhavaram, Mathavaram, Thiruvallur District, Tamil Nadu, India"
    },
    {
      "address": "West Zone, Bengaluru, Bangalore North, Bangalore Urban, Karnataka, India"
    },
    {
      "address": "Zone 4 Tondiarpet, Chennai District, Tamil Nadu, India"
    },
    {
      "address": "Greater Hyderabad Municipal Corporation East Zone, Hyderabad, Uppal mandal, Medchal–Malkajgiri, Telangana, India"
    },
    {
      "address": "Zone 12 Alandur, Alandur, Tamil Nadu, India"
    },
    {
      "address": "Greater Hyderabad Municipal Corporation South Zone, Hyderabad, Bahadurpura mandal, Hyderabad, Telangana, India"
    },
    {
      "address": "Greater Hyderabad Municipal Corporation Central Zone, Hyderabad, Khairatabad mandal, Hyderabad, Telangana, India"
    }
  ]
}
```
