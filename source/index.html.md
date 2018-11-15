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
  "user_id": 1,
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
      "amount_local": 380,
      "currency_local": "MXN",
      "provider": "FEDEX",
      "service_level_name": "Standard Overnight",
      "service_level_code": "STANDARD_OVERNIGHT",
      "trackable": null,
      "days": 1,
      "insurance_currency": "NMP",
      "insurance_commission": 70,
      "insurance_deductible": 0.01,
      "self_insurance": true
  },
  {
      "amount_local": 420,
      "currency_local": "MXN",
      "provider": "UPS",
      "service_level_name": "UPS Standard",
      "service_level_code": "STANDARD",
      "trackable": true,
      "days": 5,
      "insurance_currency": "MXN",
      "insurance_commission": 70,
      "insurance_deductible": 0.01,
      "self_insurance": false
  }
]
```

This endpoint receive an user, zip codes and parcel measures. It returns a list that
contains all Rates found.

### HTTP Request

`GET https://api.srenvio.com/v1/quotations`

### Parameters

Field | Type | Description
--------- | ------- | -----------
**user_id** | Integer | User account ID, used to load available rate carriers.
**zip_from** | String(5) | Zip code of origin.
**zip_to** | String(5) | Zip code of destination.
**parcel** | JSON | Used to specify the measures and total Parcel weight .
**weight** | Integer | Weight of Parcel, must be in KG.
**height** | Integer | Height of Parcel, must be in CM.
**width** | Integer | Width of Parcel, must be in CM.
**length** | Integer | Length of Parcel, must be in CM.

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
      "id": "1867",
      "type": "shipments",
      "attributes": {
        "status": "SUCCESS",
        "created_at": "2018-09-04T13:11:57.662-05:00",
        "updated_at": "2018-09-04T13:13:25.060-05:00"
      },
      "relationships": {
        "parcel": {
          "data": {
            "id": "533",
            "type": "parcels"
          }
        },
        "rates": {
          "data": [
            {
              "id": "11892",
              "type": "rates"
            },
            {
              "id": "11891",
              "type": "rates"
            }
          ]
        },
        "address_to": {
          "data": {
            "id": "1893",
            "type": "addresses"
          }
        },
        "address_from": {
          "data": {
            "id": "1892",
            "type": "addresses"
          }
        },
        "label": {
          "data": {
            "id": "412",
            "type": "labels"
          }
        }
      }
    }
  ],
  "included": [
    {
      "id": "533",
      "type": "parcels",
      "attributes": {
        "length": "29.7",
        "height": "21.0",
        "width": "5.0",
        "weight": "0.5",
        "mass_unit": "KG",
        "distance_unit": "CM"
      }
    },
    {
      "id": "11892",
      "type": "rates",
      "attributes": {
        "created_at": "2018-09-04T13:12:08.217-05:00",
        "updated_at": "2018-09-04T13:12:08.217-05:00",
        "amount_local": "98.0",
        "currency_local": "MXN",
        "provider": "SENDEX",
        "service_level_name": "Regular",
        "service_level_code": "REG",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null
      }
    },
    {
      "id": "11891",
      "type": "rates",
      "attributes": {
        "created_at": "2018-09-04T13:12:08.176-05:00",
        "updated_at": "2018-09-04T13:12:08.176-05:00",
        "amount_local": "228.0",
        "currency_local": "MXN",
        "provider": "REDPACK",
        "service_level_name": "Express",
        "service_level_code": "EXPRESS",
        "service_level_terms": null,
        "days": 2,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null
      }
    },
    {
      "id": "1893",
      "type": "addresses",
      "attributes": {
        "name": "Sr. Alberto Suárez Reyes",
        "company": "Suple Max",
        "address1": "Glorieta Gerardo 751 Planta alta",
        "address2": "Centro",
        "city": "Monterrey",
        "province": "Nuevo León",
        "zip": "64926",
        "country": "MX",
        "phone": "7413806700",
        "email": "ejemplo@srenvio.com",
        "created_at": "2018-09-04T13:11:57.685-05:00",
        "updated_at": "2018-09-04T13:11:57.685-05:00"
      }
    },
    {
      "id": "1892",
      "type": "addresses",
      "attributes": {
        "name": "Rosario Varela Escamilla",
        "company": "Foo Bar Company",
        "address1": "Privada Carbo 40010",
        "address2": "Centro",
        "city": "Monterrey",
        "province": "Nuevo León",
        "zip": "64000",
        "country": "MX",
        "phone": "8181818181",
        "email": "ejemplo@srenvio.com",
        "created_at": "2018-09-04T13:11:57.680-05:00",
        "updated_at": "2018-09-04T13:11:57.680-05:00"
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
    "id": "1867",
    "type": "shipments",
    "attributes": {
      "status": "SUCCESS",
      "created_at": "2018-09-04T13:11:57.662-05:00",
      "updated_at": "2018-09-04T13:13:25.060-05:00"
    },
    "relationships": {
      "parcel": {
        "data": {
          "id": "533",
          "type": "parcels"
        }
      },
      "rates": {
        "data": [
          {
            "id": "11892",
            "type": "rates"
          },
          {
            "id": "11891",
            "type": "rates"
          }
        ]
      },
      "address_to": {
        "data": {
          "id": "1893",
          "type": "addresses"
        }
      },
      "address_from": {
        "data": {
          "id": "1892",
          "type": "addresses"
        }
      },
      "label": {
        "data": {
          "id": "412",
          "type": "labels"
        }
      }
    }
  },
  "included": [
    {
      "id": "533",
      "type": "parcels",
      "attributes": {
        "length": "29.7",
        "height": "21.0",
        "width": "5.0",
        "weight": "0.5",
        "mass_unit": "KG",
        "distance_unit": "CM"
      }
    },
    {
      "id": "11892",
      "type": "rates",
      "attributes": {
        "created_at": "2018-09-04T13:12:08.217-05:00",
        "updated_at": "2018-09-04T13:12:08.217-05:00",
        "amount_local": "98.0",
        "currency_local": "MXN",
        "provider": "SENDEX",
        "service_level_name": "Regular",
        "service_level_code": "REG",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null
      }
    },
    {
      "id": "11891",
      "type": "rates",
      "attributes": {
        "created_at": "2018-09-04T13:12:08.176-05:00",
        "updated_at": "2018-09-04T13:12:08.176-05:00",
        "amount_local": "228.0",
        "currency_local": "MXN",
        "provider": "REDPACK",
        "service_level_name": "Express",
        "service_level_code": "EXPRESS",
        "service_level_terms": null,
        "days": 2,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null
      }
    },
    {
      "id": "1893",
      "type": "addresses",
      "attributes": {
        "name": "Sr. Alberto Suárez Reyes",
        "company": "Suple Max",
        "address1": "Glorieta Gerardo 751 Planta alta",
        "address2": "Centro",
        "city": "Monterrey",
        "province": "Nuevo León",
        "zip": "64926",
        "country": "MX",
        "phone": "7413806700",
        "email": "ejemplo@srenvio.com",
        "created_at": "2018-09-04T13:11:57.685-05:00",
        "updated_at": "2018-09-04T13:11:57.685-05:00"
      }
    },
    {
      "id": "1892",
      "type": "addresses",
      "attributes": {
        "name": "Rosario Varela Escamilla",
        "company": "Foo Bar Company",
        "address1": "Privada Carbo 40010",
        "address2": "Centro",
        "city": "Monterrey",
        "province": "Nuevo León",
        "zip": "64000",
        "country": "MX",
        "phone": "8181818181",
        "email": "e`",
        "created_at": "2018-09-04T13:11:57.680-05:00",
        "updated_at": "2018-09-04T13:11:57.680-05:00"
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
      "name": "Jorge Morales",
      "company": "srenvio",
      "address1": "Constitución",
      "address2": "9125",
      "city": "Monterrey",
      "province": "Monterrey",
      "zip": "64000",
      "country": "MX",
      "phone": "8181818181",
      "email": "ejemplo@srenvio.com"
    },
    "address_to": {
      "name": "Beto Rincón",
      "company": "Roplasti",
      "address1": "Av. Garza Sada",
      "address2": "9113",
      "city": "Monterrey",
      "province": "Monterrey",
      "zip": "64700",
      "country": "MX",
      "phone": "8181818181",
      "email": "ejemplo@srenvio.com",
      "contents": "Suplementos"
    },
    "parcels": [
      {
        "length": 10,
        "height": 10,
        "width": 10,
        "weight": 10,
        "mass_unit": "KG",
        "distance_unit": "CM"
      }
    ]
  }'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "1869",
    "type": "shipments",
    "attributes": {
      "status": "WAITING",
      "created_at": "2018-09-04T15:13:16.250-05:00",
      "updated_at": "2018-09-04T15:13:16.250-05:00"
    },
    "relationships": {
      "parcel": {
        "data": {
          "id": "535",
          "type": "parcels"
        }
      },
      "rates": {
        "data": [
          {
            "id": "11906",
            "type": "rates"
          },
          {
            "id": "11907",
            "type": "rates"
          }
        ]
      },
      "address_to": {
        "data": {
          "id": "1897",
          "type": "addresses"
        }
      },
      "address_from": {
        "data": {
          "id": "1896",
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
      "id": "535",
      "type": "parcels",
      "attributes": {
        "length": "10.0",
        "height": "10.0",
        "width": "10.0",
        "weight": "10.0",
        "mass_unit": "KG",
        "distance_unit": "CM"
      }
    },
    {
      "id": "11917",
      "type": "rates",
      "attributes": {
        "created_at": "2018-09-04T15:13:16.552-05:00",
        "updated_at": "2018-09-04T15:13:16.552-05:00",
        "amount_local": "119.0",
        "currency_local": "MXN",
        "provider": "SENDEX",
        "service_level_name": "Regular",
        "service_level_code": "REG",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null
      }
    },
    {
      "id": "11918",
      "type": "rates",
      "attributes": {
        "created_at": "2018-09-04T15:13:17.422-05:00",
        "updated_at": "2018-09-04T15:13:17.422-05:00",
        "amount_local": "89.0",
        "currency_local": "MXN",
        "provider": "CARSSA",
        "service_level_name": "Nacional",
        "service_level_code": "NACIONAL",
        "service_level_terms": null,
        "days": 5,
        "duration_terms": null,
        "zone": null,
        "arrives_by": null
      }
    },
    {
      "id": "1897",
      "type": "addresses",
      "attributes": {
        "name": "Beto Rincón",
        "company": "Roplasti",
        "address1": "Av. Garza Sada",
        "address2": "9113",
        "city": "Monterrey",
        "province": "Monterrey",
        "zip": "64700",
        "country": "MX",
        "phone": "8181818181",
        "email": "ejemplo@srenvio.com",
        "created_at": "2018-09-04T15:13:16.244-05:00",
        "updated_at": "2018-09-04T15:13:16.244-05:00"
      }
    },
    {
      "id": "1896",
      "type": "addresses",
      "attributes": {
        "name": "Jorge Morales",
        "company": "srenvio",
        "address1": "Constitución",
        "address2": "9125",
        "city": "Monterrey",
        "province": "Monterrey",
        "zip": "64000",
        "country": "MX",
        "phone": "8181818181",
        "email": "ejemplo@srenvio.com",
        "created_at": "2018-09-04T15:13:16.239-05:00",
        "updated_at": "2018-09-04T15:13:16.239-05:00"
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
