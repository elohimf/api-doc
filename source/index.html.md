---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://www.srenvio.com/users/sign_up'>Sign Up for an API Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Srenvio API

Welcome to the Srenvio API! You can use our API to access Srenvio API endpoints,
which can get information about Shipments and Labels, also create Cancel Label Requests.

You can view code examples in the dark area to the right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.srenvio.com/v1/shipments"
  -H "Authorization: Token token=YOUR_API_KEY"
```


> Make sure to replace `YOUR_API_KEY` with your API key.

Srenvio uses API keys to allow access to the API. You need to contact our support
team to get your API key. [hola@srenvio.com](mailto:hola@srenvio.com)

Srenvio expects for the API key to be included in all API requests to the server
in a header that looks like the following:

`Authorization: Token token=YOUR_API_KEY`

<aside class="notice">
You must replace <code>YOUR_API_KEY</code> with your personal API key.
</aside>

# Developer Testing

We recommend to use our demo environment before run your code in production.

  1. Firstly, you need to register in demo environment [here](https://demo.srenvio.com/users/sign_up).
  2. Contact our support team to get your API key.

The URL for demo environment is:

`https://api-demo.srenvio.com/`

# Quotations

## Get a Quotation

> curl:

```shell
curl "https://api.srenvio.com/v1/quotations"
  -H "Authorization: Token token=YOUR_API_KEY"
```

> Example of JSON structure sent:

```json
{
  "zip_from": "91000",
  "zip_to": "64000",
  "parcel": {
    "weight": 10,
    "height": 10,
    "width": 10,
    "length": 10
  }
}
```

> The above command returns JSON structured like this:

```json
[
  {
    "amount_local": 540,
    "currency": "MXN",
    "provider": "UPS",
    "service_level_name": "UPS Express",
    "service_level_code": "EXPRESS_SAVER",
    "days": 2,
    "insurable": false,
    "out_of_area_service": false,
    "out_of_area_pricing": 0,
    "total_pricing": 540
  },
  {
    "amount_local": 681,
    "currency": "MXN",
    "provider": "ESTAFETA",
    "service_level_name": "Servicio Express",
    "service_level_code": "ESTAFETA_NEXT_DAY",
    "days": 2,
    "insurable": true,
    "out_of_area_service": true,
    "out_of_area_pricing": 100,
    "total_pricing": 781
  }
]
```

This endpoint receives zip codes and parcel measures. It returns a list that
contains all Rates found.

### HTTP Request

`POST https://api.srenvio.com/v1/quotations`

### Parameters

Field | Type | Description
--------- | ------- | -----------
**zip_from** | String(5) | Zip code of origin.
**zip_to** | String(5) | Zip code of destination.
**parcel** | JSON | Used to specify the measures and total Parcel weight.
**weight** | Integer | Weight of Parcel, must be in KG.
**height** | Integer | Height of Parcel, must be in CM.
**width** | Integer | Width of Parcel, must be in CM.
**length** | Integer | Length of Parcel, must be in CM.


### Description
The field `amount_local` is used to indicate the price of the service.
Depending on the zip code, they may have extra charges.

Out of area means that zone is not covered for normal delivery and generates
extra charges.

`out_of_area_service` is used to indicate if the service is out of the area for
normal delivery and if it's true.

`out_of_area_pricing` have the pricing for this extra service.

`total_pricing` have the sum of `amount_local` and `out_of_area_pricing`.

`days` Estimated time of arrival.

`insurable` means that the shipment could be
insured declaring a cost. Not implemented yet in this API version.

# Shipments

## Get All Shipments

```shell
curl "https://api.srenvio.com/v1/shipments"
  -H "Authorization: Token token=YOUR_API_KEY"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "902675",
      "type": "shipments",
      "attributes": {
        "status": "WAITING",
        "created_at": "2018-12-18T15:00:21.892-06:00",
        "updated_at": "2018-12-18T15:00:21.892-06:00"
      },
      "relationships": {
        "parcel": {
          "data": {
            "id": "773773",
            "type": "parcels"
          }
        },
        "rates": {
          "data": [
            {
              "id": "7146458",
              "type": "rates"
            },
            {
              "id": "7146457",
              "type": "rates"
            },
            {
              "id": "7146456",
              "type": "rates"
            },
            {
              "id": "7146455",
              "type": "rates"
            },
            {
              "id": "7146454",
              "type": "rates"
            }
          ]
        },
        "address_to": {
          "data": {
            "id": "2901622",
            "type": "addresses"
          }
        },
        "address_from": {
          "data": {
            "id": "2901621",
            "type": "addresses"
          }
        },
        "label": {
          "data": null
        }
      }
    }
  ],
  "included": [
    {
      "id": "773773",
      "type": "parcels",
      "attributes": {
        "length": "10.0",
        "height": "10.0",
        "width": "10.0",
        "weight": "3.0",
        "mass_unit": "KG",
        "distance_unit": "CM"
      }
    },
    {
      "id": "7146458",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.418-06:00",
        "updated_at": "2018-12-18T15:00:22.418-06:00",
        "amount_local": "119.0",
        "currency_local": "MXN",
        "provider": "CARSSA",
        "service_level_name": "Nacional",
        "service_level_code": "NACIONAL",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": false,
        "out_of_area_pricing": "0.0",
        "total_pricing": "119.0"
      }
    },
    {
      "id": "7146457",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.389-06:00",
        "updated_at": "2018-12-18T15:00:22.389-06:00",
        "amount_local": "204.0",
        "currency_local": "MXN",
        "provider": "DHL",
        "service_level_name": "DHL Express",
        "service_level_code": "EXPRESS",
        "service_level_terms": null,
        "days": 2,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "349.0"
      }
    },
    {
      "id": "7146456",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.380-06:00",
        "updated_at": "2018-12-18T15:00:22.380-06:00",
        "amount_local": "180.0",
        "currency_local": "MXN",
        "provider": "DHL",
        "service_level_name": "DHL Terrestre",
        "service_level_code": "STANDARD",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "325.0"
      }
    },
    {
      "id": "7146455",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.150-06:00",
        "updated_at": "2018-12-18T15:00:22.150-06:00",
        "amount_local": "205.0",
        "currency_local": "MXN",
        "provider": "FEDEX",
        "service_level_name": "Standard Overnight",
        "service_level_code": "STANDARD_OVERNIGHT",
        "service_level_terms": null,
        "days": 2,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "350.0"
      }
    },
    {
      "id": "7146454",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.141-06:00",
        "updated_at": "2018-12-18T15:00:22.141-06:00",
        "amount_local": "149.0",
        "currency_local": "MXN",
        "provider": "FEDEX",
        "service_level_name": "Fedex Express Saver",
        "service_level_code": "FEDEX_EXPRESS_SAVER",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "294.0"
      }
    },
    {
      "id": "2901622",
      "type": "addresses",
      "attributes": {
        "name": "Jorge Fernández",
        "company": "-",
        "address1": "Av. Lázaro Cárdenas #234",
        "address2": "Americana",
        "city": "Guadalajara",
        "province": "Jalisco",
        "zip": "23312",
        "country": "MXN",
        "phone": "3311510605",
        "email": "ejemplo@srenvio.com",
        "created_at": "2018-12-18T15:00:21.887-06:00",
        "updated_at": "2018-12-18T15:00:21.887-06:00"
      }
    },
    {
      "id": "2901621",
      "type": "addresses",
      "attributes": {
        "name": "Jose Fernando",
        "company": "srenvio",
        "address1": "Av. Principal #234",
        "address2": "Centro",
        "city": "Guadalajara",
        "province": "Jalisco",
        "zip": "02900",
        "country": "MXN",
        "phone": "3384217447",
        "email": "srenvio@email.com",
        "created_at": "2018-12-18T15:00:21.874-06:00",
        "updated_at": "2018-12-18T15:00:21.874-06:00"
      }
    }
  ],
  "links": {
    "self": "https://api.srenvio.com/v1/shipments?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "first": "https://api.srenvio.com/v1/shipments?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "prev": null,
    "next": null,
    "last": "https://api.srenvio.com/v1/shipments?page%5Bnumber%5D=1&page%5Bsize%5D=20"
  }
}
```

This endpoint retrieves all Shipments.

### HTTP Request

`GET https://api.srenvio.com/v1/shipments`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page[number] | 1 | Number of page.
page[size] | 20 | Quantity of records per page.

<aside class="success">
At the end of the returned JSON there are some links to get the previous and next
data. Also the current, first and last link page.
</aside>

## Get a Specific Shipment

```shell
curl "GET https://api.srenvio.com/v1/shipments/<ID>"
  -H "Authorization: Token token=YOUR_API_KEY"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "902675",
    "type": "shipments",
    "attributes": {
      "status": "WAITING",
      "created_at": "2018-12-18T15:00:21.892-06:00",
      "updated_at": "2018-12-18T15:00:21.892-06:00"
    },
    "relationships": {
      "parcel": {
        "data": {
          "id": "773773",
          "type": "parcels"
        }
      },
      "rates": {
        "data": [
          {
            "id": "7146458",
            "type": "rates"
          },
          {
            "id": "7146457",
            "type": "rates"
          },
          {
            "id": "7146456",
            "type": "rates"
          },
          {
            "id": "7146455",
            "type": "rates"
          },
          {
            "id": "7146454",
            "type": "rates"
          }
        ]
      },
      "address_to": {
        "data": {
          "id": "2901622",
          "type": "addresses"
        }
      },
      "address_from": {
        "data": {
          "id": "2901621",
          "type": "addresses"
        }
      },
      "label": {
        "data": null
      }
    }
  },
  "included": [
    {
      "id": "773773",
      "type": "parcels",
      "attributes": {
        "length": "10.0",
        "height": "10.0",
        "width": "10.0",
        "weight": "3.0",
        "mass_unit": "KG",
        "distance_unit": "CM"
      }
    },
    {
      "id": "7146458",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.418-06:00",
        "updated_at": "2018-12-18T15:00:22.418-06:00",
        "amount_local": "119.0",
        "currency_local": "MXN",
        "provider": "CARSSA",
        "service_level_name": "Nacional",
        "service_level_code": "NACIONAL",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": false,
        "out_of_area_pricing": "0.0",
        "total_pricing": "119.0"
      }
    },
    {
      "id": "7146457",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.389-06:00",
        "updated_at": "2018-12-18T15:00:22.389-06:00",
        "amount_local": "204.0",
        "currency_local": "MXN",
        "provider": "DHL",
        "service_level_name": "DHL Express",
        "service_level_code": "EXPRESS",
        "service_level_terms": null,
        "days": 2,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "349.0"
      }
    },
    {
      "id": "7146456",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.380-06:00",
        "updated_at": "2018-12-18T15:00:22.380-06:00",
        "amount_local": "180.0",
        "currency_local": "MXN",
        "provider": "DHL",
        "service_level_name": "DHL Terrestre",
        "service_level_code": "STANDARD",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "325.0"
      }
    },
    {
      "id": "7146455",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.150-06:00",
        "updated_at": "2018-12-18T15:00:22.150-06:00",
        "amount_local": "205.0",
        "currency_local": "MXN",
        "provider": "FEDEX",
        "service_level_name": "Standard Overnight",
        "service_level_code": "STANDARD_OVERNIGHT",
        "service_level_terms": null,
        "days": 2,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "350.0"
      }
    },
    {
      "id": "7146454",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.141-06:00",
        "updated_at": "2018-12-18T15:00:22.141-06:00",
        "amount_local": "149.0",
        "currency_local": "MXN",
        "provider": "FEDEX",
        "service_level_name": "Fedex Express Saver",
        "service_level_code": "FEDEX_EXPRESS_SAVER",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "294.0"
      }
    },
    {
      "id": "2901622",
      "type": "addresses",
      "attributes": {
        "name": "Jorge Fernández",
        "company": "-",
        "address1": "Av. Lázaro Cárdenas #234",
        "address2": "Americana",
        "city": "Guadalajara",
        "province": "Jalisco",
        "zip": "23312",
        "country": "MXN",
        "phone": "3311510605",
        "email": "ejemplo@srenvio.com",
        "created_at": "2018-12-18T15:00:21.887-06:00",
        "updated_at": "2018-12-18T15:00:21.887-06:00"
      }
    },
    {
      "id": "2901621",
      "type": "addresses",
      "attributes": {
        "name": "Jose Fernando",
        "company": "srenvio",
        "address1": "Av. Principal #234",
        "address2": "Centro",
        "city": "Guadalajara",
        "province": "Jalisco",
        "zip": "02900",
        "country": "MXN",
        "phone": "3384217447",
        "email": "srenvio@email.com",
        "created_at": "2018-12-18T15:00:21.874-06:00",
        "updated_at": "2018-12-18T15:00:21.874-06:00"
      }
    }
  ]
}

```

This endpoint retrieves a specific Shipment.

### HTTP Request

`GET https://api.srenvio.com/v1/shipments/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Shipment to retrieve

## Create a Shipment

> Example of create a Shipment:

```shell
curl "https://api.srenvio.com/v1/shipments"
  -H "Authorization: Token token=YOUR_API_KEY"
  -H "Content-Type: application/json" \
  -d '{
      "address_from": {
      "province": "Jalisco",
      "city": "Guadalajara",
      "name": "Jose Fernando",
      "zip": "02900",
      "country": "MXN",
      "address1": "Av. Principal #234",
      "company": "srenvio",
      "address2": "Centro",
      "phone": "3384217447",
      "email": "srenvio@email.com"},
      "parcels": [{
        "weight": 3,
        "distance_unit": "CM",
        "mass_unit": "KG",
        "height": 10,
        "width": 10,
        "length": 10
      }],
      "address_to": {
        "province": "Jalisco",
        "city": "Guadalajara",
        "name": "Jorge Fernández",
        "zip": "23312",
        "country": "MXN",
        "address1": " Av. Lázaro Cárdenas #234",
        "company": "-",
        "address2": "Americana",
        "phone": "3311510605",
        "email": "ejemplo@srenvio.com"
      }
    }'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "902675",
    "type": "shipments",
    "attributes": {
      "status": "WAITING",
      "created_at": "2018-12-18T15:00:21.892-06:00",
      "updated_at": "2018-12-18T15:00:21.892-06:00"
    },
    "relationships": {
      "parcel": {
        "data": {
          "id": "773773",
          "type": "parcels"
        }
      },
      "rates": {
        "data": [
          {
            "id": "7146454",
            "type": "rates"
          },
          {
            "id": "7146455",
            "type": "rates"
          },
          {
            "id": "7146456",
            "type": "rates"
          },
          {
            "id": "7146457",
            "type": "rates"
          },
          {
            "id": "7146458",
            "type": "rates"
          }
        ]
      },
      "address_to": {
        "data": {
          "id": "2901622",
          "type": "addresses"
        }
      },
      "address_from": {
        "data": {
          "id": "2901621",
          "type": "addresses"
        }
      },
      "label": {
        "data": null
      }
    }
  },
  "included": [
    {
      "id": "773773",
      "type": "parcels",
      "attributes": {
        "length": "10.0",
        "height": "10.0",
        "width": "10.0",
        "weight": "3.0",
        "mass_unit": "KG",
        "distance_unit": "CM"
      }
    },
    {
      "id": "7146454",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.141-06:00",
        "updated_at": "2018-12-18T15:00:22.141-06:00",
        "amount_local": "149.0",
        "currency_local": "MXN",
        "provider": "FEDEX",
        "service_level_name": "Fedex Express Saver",
        "service_level_code": "FEDEX_EXPRESS_SAVER",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "294.0"
      }
    },
    {
      "id": "7146455",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.150-06:00",
        "updated_at": "2018-12-18T15:00:22.150-06:00",
        "amount_local": "205.0",
        "currency_local": "MXN",
        "provider": "FEDEX",
        "service_level_name": "Standard Overnight",
        "service_level_code": "STANDARD_OVERNIGHT",
        "service_level_terms": null,
        "days": 2,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "350.0"
      }
    },
    {
      "id": "7146456",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.380-06:00",
        "updated_at": "2018-12-18T15:00:22.380-06:00",
        "amount_local": "180.0",
        "currency_local": "MXN",
        "provider": "DHL",
        "service_level_name": "DHL Terrestre",
        "service_level_code": "STANDARD",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "325.0"
      }
    },
    {
      "id": "7146457",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.389-06:00",
        "updated_at": "2018-12-18T15:00:22.389-06:00",
        "amount_local": "204.0",
        "currency_local": "MXN",
        "provider": "DHL",
        "service_level_name": "DHL Express",
        "service_level_code": "EXPRESS",
        "service_level_terms": null,
        "days": 2,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": true,
        "out_of_area_pricing": "145.00",
        "total_pricing": "349.0"
      }
    },
    {
      "id": "7146458",
      "type": "rates",
      "attributes": {
        "created_at": "2018-12-18T15:00:22.418-06:00",
        "updated_at": "2018-12-18T15:00:22.418-06:00",
        "amount_local": "119.0",
        "currency_local": "MXN",
        "provider": "CARSSA",
        "service_level_name": "Nacional",
        "service_level_code": "NACIONAL",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null,
        "out_of_area": false,
        "out_of_area_pricing": "0.0",
        "total_pricing": "119.0"
      }
    },
    {
      "id": "2901622",
      "type": "addresses",
      "attributes": {
        "name": "Jorge Fernández",
        "company": "-",
        "address1": "Av. Lázaro Cárdenas #234",
        "address2": "Americana",
        "city": "Guadalajara",
        "province": "Jalisco",
        "zip": "23312",
        "country": "MXN",
        "phone": "3311510605",
        "email": "ejemplo@srenvio.com",
        "created_at": "2018-12-18T15:00:21.887-06:00",
        "updated_at": "2018-12-18T15:00:21.887-06:00"
      }
    },
    {
      "id": "2901621",
      "type": "addresses",
      "attributes": {
        "name": "Jose Fernando",
        "company": "srenvio",
        "address1": "Av. Principal #234",
        "address2": "Centro",
        "city": "Guadalajara",
        "province": "Jalisco",
        "zip": "02900",
        "country": "MXN",
        "phone": "3384217447",
        "email": "srenvio@email.com",
        "created_at": "2018-12-18T15:00:21.874-06:00",
        "updated_at": "2018-12-18T15:00:21.874-06:00"
      }
    }
  ]
}
```

This endpoint creates a Shipment.

### HTTP Request

`POST https://api.srenvio.com/v1/shipments`

# Labels

## Get All Labels

```shell
curl "https://api.srenvio.com/v1/labels"
  -H "Authorization: Token token=YOUR_API_KEY"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "39",
      "type": "labels",
      "attributes": {
        "created_at": "2018-07-26T00:18:56.665-05:00",
        "updated_at": "2018-07-26T00:18:56.665-05:00",
        "status": null,
        "tracking_number": "XXXXXXXXXX",
        "tracking_status": null,
        "label_url": "label-url.pdf",
        "tracking_url_provider": "http://www.estafeta.com/Rastreo/XXXXXXXXXX",
        "rate_id": 3087
      }
    },
    {
      "id": "40",
      "type": "labels",
      "attributes": {
        "created_at": "2018-07-26T00:18:57.326-05:00",
        "updated_at": "2018-07-26T00:18:57.326-05:00",
        "status": null,
        "tracking_number": "XXXXXXXXXX",
        "tracking_status": null,
        "label_url": "label-url.pdf",
        "tracking_url_provider": "http://www.estafeta.com/Rastreo/XXXXXXXXXX",
        "rate_id": 3089
      }
    }
  ],
  "links": {
    "self": "https://api.srenvio.com/v1/labels?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "first": "https://api.srenvio.com/v1/labels?page%5Bnumber%5D=1&page%5Bsize%5D=20",
    "prev": null,
    "next": "https://api.srenvio.com/v1/labels?page%5Bnumber%5D=2&page%5Bsize%5D=20",
    "last": "https://api.srenvio.com/v1/labels?page%5Bnumber%5D=13&page%5Bsize%5D=20"
  }
}
```

This endpoint retrieves all Labels.

### HTTP Request

`GET https://api.srenvio.com/v1/labels`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page[number] | 1 | Number of page.
page[size] | 20 | Quantity of records per page.

<aside class="success">
At the end of the returned JSON there are some links to get the previous and next
data. Also the current, first and last link page.
</aside>


## Get a Specific Label

```shell
curl "GET https://api.srenvio.com/v1/labels/<ID>"
  -H "Authorization: Token token=YOUR_API_KEY"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "2",
    "type": "labels",
    "attributes": {
      "created_at": "2018-07-18T16:05:05.370-05:00",
      "updated_at": "2018-07-18T16:05:05.370-05:00",
      "status": null,
      "tracking_number": "XXXXXXXXXX",
      "tracking_status": null,
      "label_url": "label-url.pdf",
      "tracking_url_provider": "https://www.fedex.com/apps/fedextrack/?action=track&trackingnumber=XXXXXXXXXX",
      "rate_id": 3
    }
  }
}

```

This endpoint retrieves a specific Label.


### HTTP Request

`GET https://api.srenvio.com/v1/labels/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Label to retrieve


## Create a Label

> Example of create a Label:

```shell
curl "https://api.srenvio.com/v1/labels"
  -H "Authorization: Token token=YOUR_API_KEY"
  -H "Content-Type: application/json" \
  -d '{
    "rate_id": 10834,
    "label_format": "pdf"
  }'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "414",
    "type": "labels",
    "attributes": {
      "created_at": "2018-09-04T16:32:49.190-05:00",
      "updated_at": "2018-09-04T16:32:49.190-05:00",
      "status": null,
      "tracking_number": "XXXXXXXXXX",
      "tracking_status": null,
      "label_url": "label-url.pdf",
      "tracking_url_provider": "https://www.grupocarssa.com/new/XXXXXXXXXX",
      "rate_id": 11931
    }
  }
}
```

This endpoint creates a Label.

### HTTP Request

`POST https://api.srenvio.com/v1/labels`

# Cancel Label Request

## Create a Cancel Label Request

> Example of create a Cancel Label Request:

```shell
curl "https://api.srenvio.com/v1/cancel_label_requests"
  -H "Authorization: Token token=YOUR_API_KEY"
  -H "Content-Type: application/json" \
  -d '{
    "tracking_number": "XXXXXXXXXX",
    "reason": "Datos de dirección erróneos."
  }'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "18",
    "type": "cancel_requests",
    "attributes": {
      "status": "reviewing",
      "reason": "Datos de dirección erróneos.",
      "created_at": "2018-09-05T09:24:35.453-05:00",
      "updated_at": "2018-09-05T09:24:35.453-05:00"
    }
  }
}
```

This endpoint creates a Cancel Label Request.

### HTTP Request

`POST https://api.srenvio.com/v1/cancel_label_requests`
