# Customers

Customer objects allow you to perform recurring charges and track multiple charges that are associated with the same customer. The API allows you to create, delete, and update your customers. You can retrieve individual customers as well as a list of all your customers.

## The customer object

> ### Example Response

```json
{
  "id": "cust_zAiRxC7b3N2bc0Q6",
  "object": "customer",
  "livemode": false,
  "created_at": 1443083832,
  "email": "tofupay125@tofu.com",
  "description": null,
  "default_card": "card_yaurbcUKmRaCw4fuKaoptl1K",
  "url": "/v1/customers/cust_zAiRxC7b3N2bc0Q6/payment_methods",
  "payment_methods": {
    "data": [
      {
        "id": "card_yaurbcUKmRaCw4fuKaoptl1K",
        "object": "card",
        "created_at": 1443083815,
        "brand": "visa",
        "last_four": 4242,
        "exp_month": 12,
        "exp_year": 2016,
        "holder_name": "Tofu Pay",
        "country": null,
        "address_1": "123",
        "address_2": null,
        "address_city": "Hong Kong",
        "address_country": "Hong Kong",
        "address_postcode": null,
        "customer": "cust_zAiRxC7b3N2bc0Q6"
      }
    ]
  }
}
```

### Parameters

Parameter | Type | Description
--------- | ------- | ----------- | -----------
id | string | The ID of the customer.
object |  string | 'customer'
created_at | timestamp | Time of creation
livemode | boolean | True - live, False - sandbox
email | string | Email address of the client.
description | string | Description of the customer.
default_card | string | The ID of payment card.
payment_methods | list | List of the registered payment methods.





## Create a customer

> ### DEFINITION
> POST https://sandbox.tofupay.com/v1/customers
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/customers \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT: \
   -d description="Customer for test@example.com" \
   -d source=tok_15XZLsLdZh7jQOUq86ISvtjn
```

```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

Tofupay::Customer.create(
  :description => "Customer for test@example.com",
  :source => "tok_15XZLsLdZh7jQOUq86ISvtjn" # obtained with Tofupay.js
)
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

tofupay.Customer.create(
  description="Customer for test@example.com",
  source="tok_15XZLsLdZh7jQOUq86ISvtjn" # obtained with Tofupay.js
)
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

\Tofupay\Customer::create(array(
  "description" => "Customer for test@example.com",
  "source" => "tok_15XZLsLdZh7jQOUq86ISvtjn" // obtained with Tofupay.js
));
```

> ### Example Response

```json
{
  "id": "cust_zAiRxC7b3N2bc0Q6",
  "object": "customer",
  "livemode": false,
  "created_at": 1443083832,
  "email": "tofupay125@tofu.com",
  "description": null,
  "default_card": "card_yaurbcUKmRaCw4fuKaoptl1K",
  "url": "/v1/customers/cust_zAiRxC7b3N2bc0Q6/payment_methods",
  "payment_methods": {
    "data": [
      {
        "id": "card_yaurbcUKmRaCw4fuKaoptl1K",
        "object": "card",
        "created_at": 1443083815,
        "brand": "visa",
        "last_four": 4242,
        "exp_month": 12,
        "exp_year": 2016,
        "holder_name": "Tofu Pay",
        "country": null,
        "address_1": "123",
        "address_2": null,
        "address_city": "Hong Kong",
        "address_country": "Hong Kong",
        "address_postcode": null,
        "customer": "cust_zAiRxC7b3N2bc0Q6"
      }
    ]
  }
}
```

Creates a new customer object.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
email | N | string | Email address.
description | N | string | Description.
payment_method | N | string | A payment card token or dictionary containing a user's credit card details.

### Returns
Returns a customer object if the call succeeded. 












## Retrieve a customer

> ### DEFINITION
> POST https://sandbox.tofupay.com/v1/customers/{CUSTOMER_ID}
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/customers/cus_5V50idQJ7fxkRX \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT:
```

```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

Tofupay::Customer.retrieve("cus_5V50idQJ7fxkRX")
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

tofupay.Customer.retrieve("cus_5V50idQJ7fxkRX")
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

\Tofupay\Customer::retrieve("cus_5V50idQJ7fxkRX");
```
> ### Example Response

```json
{
  "id": "cust_zAiRxC7b3N2bc0Q6",
  "object": "customer",
  "livemode": false,
  "created_at": 1443083832,
  "email": "tofupay125@tofu.com",
  "description": null,
  "default_card": "card_yaurbcUKmRaCw4fuKaoptl1K",
  "url": "/v1/customers/cust_zAiRxC7b3N2bc0Q6/payment_methods",
  "payment_methods": {
    "data": [
      {
        "id": "card_yaurbcUKmRaCw4fuKaoptl1K",
        "object": "card",
        "created_at": 1443083815,
        "brand": "visa",
        "last_four": 4242,
        "exp_month": 12,
        "exp_year": 2016,
        "holder_name": "Tofu Pay",
        "country": null,
        "address_1": "123",
        "address_2": null,
        "address_city": "Hong Kong",
        "address_country": "Hong Kong",
        "address_postcode": null,
        "customer": "cust_zAiRxC7b3N2bc0Q6"
      }
    ]
  }
}
```

Retrieves the details of an existing customer. You need only supply the unique customer identifier that was returned upon customer creation.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
id | Y | string | The ID of the desired customer.

### Returns
Returns a customer object if a valid identifier was provided. 













## Retrieve all customers

> ### DEFINITION
> GET https://sandbox.tofupay.com/v1/customers
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/customers?limit=3 \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT:
```

```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

Tofupay::Customer.all(:limit => 3)
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

tofupay.Customer.all(limit=3)
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

\Tofupay\Customer::all(array("limit" => 3));
```

> ### Example Response

```json
{
  "object": "list",
  "data": [
    {
      "id": "cust_rs8t9j9M-TuqDtlS",
      "object": "customer",
      "livemode": false,
      "created_at": 1433855964,
      "email": "tofu@pay.com",
      "description": null,
      "default_card": null,
      "payment_methods": {
        "data": [ ]
      }
    },
    {
      "id": "cust_UkZICUu6UcehwfVf",
      "object": "customer",
      "livemode": false,
      "created_at": 1433856023,
      "email": "tofu1@pay.com",
      "description": null,
      "default_card": "card_KtRLPsJGl5yUYWAVDnRFzCgj",
      "payment_methods": {
        "data": [
          {
            "id": "card_KtRLPsJGl5yUYWAVDnRFzCgj",
            "object": "card",
            "created_at": 1433856009,
            "brand": "visa",
            "last_four": 4242,
            "exp_month": 12,
            "exp_year": 2016,
            "holder_name": "Tofu Pay",
            "country": "HK",
            "address_1": null,
            "address_2": null,
            "address_city": null,
            "address_country": null,
            "address_postcode": null,
            "customer": "cust_UkZICUu6UcehwfVf"
          }
        ]
      }
    }
  ]
}
```

Returns a list of transactions you've previously created. The transactions are returned in sorted order, with the most recent transactions appearing first.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
limit | N | integer | Maximum number of transaction objects to be returned

### Returns
A dictionary with a data property that contains an array of up to limit transactions. Each entry in the array is a separate transaction object. If no more transactions are available, the resulting array will be empty. If you provide a non-existent customer ID, this call returns an [error](http://wosigor.github.io/slate/#errors).








## Update a customer

> ### DEFINITION
> POST https://sandbox.tofupay.com/v1/customers/{CUSTOMER_ID}
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/customers/cus_5V50idQJ7fxkRX \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT: \
   -d description="Customer for test@example.com"
```

```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

cu = Tofupay::Customer.retrieve("cus_5V50idQJ7fxkRX")
cu.description = "Customer for test@example.com"
cu.source = "tok_15XZLsLdZh7jQOUq86ISvtjn" # obtained with Tofupay.js
cu.save
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

cu = tofupay.Customer.retrieve("cus_5V50idQJ7fxkRX")
cu.description = "Customer for test@example.com"
cu.save()
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

$cu = \Tofupay\Customer::retrieve("cus_5V50idQJ7fxkRX");
$cu->description = "Customer for test@example.com";
$cu->source = "tok_15XZLsLdZh7jQOUq86ISvtjn"; // obtained with Tofupay.js
$cu->save();
```
> ### Example Response

```json
{
  "id": "cust_zAiRxC7b3N2bc0Q6",
  "object": "customer",
  "livemode": false,
  "created_at": 1443083832,
  "email": "tofupay125@tofu.com",
  "description": null,
  "default_card": "card_yaurbcUKmRaCw4fuKaoptl1K",
  "url": "/v1/customers/cust_zAiRxC7b3N2bc0Q6/payment_methods",
  "payment_methods": {
    "data": [
      {
        "id": "card_yaurbcUKmRaCw4fuKaoptl1K",
        "object": "card",
        "created_at": 1443083815,
        "brand": "visa",
        "last_four": 4242,
        "exp_month": 12,
        "exp_year": 2016,
        "holder_name": "Tofu Pay",
        "country": null,
        "address_1": "123",
        "address_2": null,
        "address_city": "Hong Kong",
        "address_country": "Hong Kong",
        "address_postcode": null,
        "customer": "cust_zAiRxC7b3N2bc0Q6"
      }
    ]
  }
}
```

Updates the specified customer by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
id | Y | String | ID of a customer
email | N | string | Email address.
description | N | string | Description.
card | N | string | A payment card token or dictionary containing a user's credit card details.

### Returns
Returns the customer object if the update succeeded. Returns an [error](http://wosigor.github.io/slate/#errors) if update parameters are invalid (e.g. specifying an invalid coupon or an invalid card).








## Delete a customer

> ### DEFINITION
> DELETE https://sandbox.tofupay.com/v1/customers/{CUSTOMER_ID}
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/customers/cus_5V50idQJ7fxkRX \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT: \
   -X DELETE
```

```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

cu = Tofupay::Customer.retrieve("cus_5V50idQJ7fxkRX")
cu.delete
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

cu = tofupay.Customer.retrieve("cus_5V50idQJ7fxkRX")
cu.delete()
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

$cu = \Tofupay\Customer::retrieve("cus_5V50idQJ7fxkRX");
$cu->delete();
```
> ### Example Response

```json
{
  "deleted": true,
  "id": "cus_5V50idQJ7fxkRX"
}
```

Permanently deletes a customer. It cannot be undone.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
id | Y | string | The ID of the customer to be deleted.

### Returns
Returns an object with a deleted parameter on success. If the customer ID does not exist, this call returns an [error](http://wosigor.github.io/slate/#errors).




