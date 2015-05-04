# Customers

Customer objects allow you to perform recurring charges and track multiple charges that are associated with the same customer. The API allows you to create, delete, and update your customers. You can retrieve individual customers as well as a list of all your customers.

## The customer object

> ### Example Response

```json
{
  "object": "customer",
  "created": 1421056271,
  "id": "cus_5V50idQJ7fxkRX",
  "livemode": false,
  "description": "kif",
  "email": "kif@hong.com",
  "delinquent": false,
  "metadata": {
  },
  "subscriptions": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/customers/cus_5V50idQJ7fxkRX/subscriptions",
    "data": [

    ]
  },
  "discount": null,
  "account_balance": 0,
  "currency": "usd",
  "sources": {
    "object": "list",
    "total_count": 1,
    "has_more": false,
    "url": "/v1/customers/cus_5V50idQJ7fxkRX/sources",
    "data": [
      {
        "id": "card_15g9tMLdZh7jQOUqZKKlKMIr",
        "object": "card",
        "last4": "4242",
        "brand": "Visa",
        "funding": "credit",
        "exp_month": 3,
        "exp_year": 2016,
        "country": "US",
        "name": null,
        "address_line1": null,
        "address_line2": null,
        "address_city": null,
        "address_state": null,
        "address_zip": null,
        "address_country": null,
        "cvc_check": "pass",
        "address_line1_check": null,
        "address_zip_check": null,
        "dynamic_last4": null,
        "metadata": {
        },
        "customer": "cus_5V50idQJ7fxkRX"
      }
    ]
  },
  "default_source": "card_15g9tMLdZh7jQOUqZKKlKMIr"
}
```

### Parameters

Parameter | Type | Description
--------- | ------- | ----------- | -----------
id | string | The ID of the customer.
object |  string | 'customer'
created | timestamp | 
| |









## Create a customer

> ### DEFINITION
> POST https://api.tofupay.com/v1/customers
> ### Example Request

```shell
curl https://api.tofupay.com/v1/customers \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc: \
   -d description="Customer for test@example.com" \
   -d source=tok_15XZLsLdZh7jQOUq86ISvtjn
```

```ruby
require "tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay::Customer.create(
  :description => "Customer for test@example.com",
  :source => "tok_15XZLsLdZh7jQOUq86ISvtjn" # obtained with Tofupay.js
)
```

```python
import tofupay
tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

tofupay.Customer.create(
  description="Customer for test@example.com",
  source="tok_15XZLsLdZh7jQOUq86ISvtjn" # obtained with Tofupay.js
)
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

\Tofupay\Customer::create(array(
  "description" => "Customer for test@example.com",
  "source" => "tok_15XZLsLdZh7jQOUq86ISvtjn" // obtained with Tofupay.js
));
```

> ### Example Response

```json
{
  "object": "customer",
  "created": 1421056271,
  "id": "cus_5V50idQJ7fxkRX",
  "livemode": false,
  "description": "kif",
  "email": "kif@hong.com",
  "delinquent": false,
  "metadata": {
  },
  "subscriptions": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/customers/cus_5V50idQJ7fxkRX/subscriptions",
    "data": [

    ]
  },
  "discount": null,
  "account_balance": 0,
  "currency": "usd",
  "sources": {
    "object": "list",
    "total_count": 1,
    "has_more": false,
    "url": "/v1/customers/cus_5V50idQJ7fxkRX/sources",
    "data": [
      {
        "id": "card_15g9tMLdZh7jQOUqZKKlKMIr",
        "object": "card",
        "last4": "4242",
        "brand": "Visa",
        "funding": "credit",
        "exp_month": 3,
        "exp_year": 2016,
        "country": "US",
        "name": null,
        "address_line1": null,
        "address_line2": null,
        "address_city": null,
        "address_state": null,
        "address_zip": null,
        "address_country": null,
        "cvc_check": "pass",
        "address_line1_check": null,
        "address_zip_check": null,
        "dynamic_last4": null,
        "metadata": {
        },
        "customer": "cus_5V50idQJ7fxkRX"
      }
    ]
  },
  "default_source": "card_15g9tMLdZh7jQOUqZKKlKMIr"
}
```

Creates a new customer object.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
email | N | string | Email address.
description | N | string | Description.
card | N | string | A payment card token or dictionary containing a user's credit card details.

### Returns
Returns a customer object if the call succeeded. 












## Retrieve a customer

```shell
curl https://api.tofupay.com/v1/customers/cus_5V50idQJ7fxkRX \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc:
```

```ruby
require "tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay::Customer.retrieve("cus_5V50idQJ7fxkRX")
```

```python
import tofupay
tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

tofupay.Customer.retrieve("cus_5V50idQJ7fxkRX")
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

\Tofupay\Customer::retrieve("cus_5V50idQJ7fxkRX");
```
> ### Example Response

```json
{
  "object": "customer",
  "created": 1421056271,
  "id": "cus_5V50idQJ7fxkRX",
  "livemode": false,
  "description": "kif",
  "email": "kif@hong.com",
  "delinquent": false,
  "metadata": {
  },
  "subscriptions": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/customers/cus_5V50idQJ7fxkRX/subscriptions",
    "data": [

    ]
  },
  "discount": null,
  "account_balance": 0,
  "currency": "usd",
  "sources": {
    "object": "list",
    "total_count": 1,
    "has_more": false,
    "url": "/v1/customers/cus_5V50idQJ7fxkRX/sources",
    "data": [
      {
        "id": "card_15g9tMLdZh7jQOUqZKKlKMIr",
        "object": "card",
        "last4": "4242",
        "brand": "Visa",
        "funding": "credit",
        "exp_month": 3,
        "exp_year": 2016,
        "country": "US",
        "name": null,
        "address_line1": null,
        "address_line2": null,
        "address_city": null,
        "address_state": null,
        "address_zip": null,
        "address_country": null,
        "cvc_check": "pass",
        "address_line1_check": null,
        "address_zip_check": null,
        "dynamic_last4": null,
        "metadata": {
        },
        "customer": "cus_5V50idQJ7fxkRX"
      }
    ]
  },
  "default_source": "card_15g9tMLdZh7jQOUqZKKlKMIr"
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
> GET https://api.tofupay.com/v1/customers
> ### Example Request

```shell
curl https://api.tofupay.com/v1/customers?limit=3 \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc:
```

```ruby
require "tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay::Customer.all(:limit => 3)
```

```python
import tofupay
tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

tofupay.Customer.all(limit=3)
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

\Tofupay\Customer::all(array("limit" => 3));
```

> ### Example Response

```json
{
  "object": "list",
  "url": "/v1/customers",
  "has_more": false,
  "data": [
    {
      "object": "customer",
      "created": 1421056271,
      "id": "cus_5V50idQJ7fxkRX",
      "livemode": false,
      "description": "kif",
      "email": "kif@hong.com",
      "delinquent": false,
      "metadata": {
      },
      "subscriptions": {
        "object": "list",
        "total_count": 0,
        "has_more": false,
        "url": "/v1/customers/cus_5V50idQJ7fxkRX/subscriptions",
        "data": [
    
        ]
      },
      "discount": null,
      "account_balance": 0,
      "currency": "usd",
      "sources": {
        "object": "list",
        "total_count": 1,
        "has_more": false,
        "url": "/v1/customers/cus_5V50idQJ7fxkRX/sources",
        "data": [
          {
            "id": "card_15g9tMLdZh7jQOUqZKKlKMIr",
            "object": "card",
            "last4": "4242",
            "brand": "Visa",
            "funding": "credit",
            "exp_month": 3,
            "exp_year": 2016,
            "country": "US",
            "name": null,
            "address_line1": null,
            "address_line2": null,
            "address_city": null,
            "address_state": null,
            "address_zip": null,
            "address_country": null,
            "cvc_check": "pass",
            "address_line1_check": null,
            "address_zip_check": null,
            "dynamic_last4": null,
            "metadata": {
            },
            "customer": "cus_5V50idQJ7fxkRX"
          }
        ]
      },
      "default_source": "card_15g9tMLdZh7jQOUqZKKlKMIr"
    },
    {...},
    {...}
  ]
}
```

Returns a list of transactions you've previously created. The transactions are returned in sorted order, with the most recent transactions appearing first.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
limit | N | integer | Maximum number of transaction objects to be returned

### Returns
A dictionary with a data property that contains an array of up to limit transactions. Each entry in the array is a separate transaction object. If no more transactions are available, the resulting array will be empty. If you provide a non-existent customer ID, this call returns an [error](https://tofupay.com/docs/api#errors).








## Update a customer

> ### DEFINITION
> POST https://api.tofupay.com/v1/customers/{CUSTOMER_ID}
> ### Example Request

```shell
curl https://api.tofupay.com/v1/customers/cus_5V50idQJ7fxkRX \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc: \
   -d description="Customer for test@example.com"
```

```ruby
require "tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

cu = Tofupay::Customer.retrieve("cus_5V50idQJ7fxkRX")
cu.description = "Customer for test@example.com"
cu.source = "tok_15XZLsLdZh7jQOUq86ISvtjn" # obtained with Tofupay.js
cu.save
```

```python
import tofupay
tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

cu = tofupay.Customer.retrieve("cus_5V50idQJ7fxkRX")
cu.description = "Customer for test@example.com"
cu.save()
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

$cu = \Tofupay\Customer::retrieve("cus_5V50idQJ7fxkRX");
$cu->description = "Customer for test@example.com";
$cu->source = "tok_15XZLsLdZh7jQOUq86ISvtjn"; // obtained with Tofupay.js
$cu->save();
```
> ### Example Response

```json
{
  "object": "customer",
  "created": 1421056271,
  "id": "cus_5V50idQJ7fxkRX",
  "livemode": false,
  "description": "Customer for test@example.com",
  "email": "kif@hong.com",
  "delinquent": false,
  "metadata": {
  },
  "subscriptions": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/customers/cus_5V50idQJ7fxkRX/subscriptions",
    "data": [

    ]
  },
  "discount": null,
  "account_balance": 0,
  "currency": "usd",
  "sources": {
    "object": "list",
    "total_count": 1,
    "has_more": false,
    "url": "/v1/customers/cus_5V50idQJ7fxkRX/sources",
    "data": [
      {
        "id": "card_15g9tMLdZh7jQOUqZKKlKMIr",
        "object": "card",
        "last4": "4242",
        "brand": "Visa",
        "funding": "credit",
        "exp_month": 3,
        "exp_year": 2016,
        "country": "US",
        "name": null,
        "address_line1": null,
        "address_line2": null,
        "address_city": null,
        "address_state": null,
        "address_zip": null,
        "address_country": null,
        "cvc_check": "pass",
        "address_line1_check": null,
        "address_zip_check": null,
        "dynamic_last4": null,
        "metadata": {
        },
        "customer": "cus_5V50idQJ7fxkRX"
      }
    ]
  },
  "default_source": "card_15g9tMLdZh7jQOUqZKKlKMIr"
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
Returns the customer object if the update succeeded. Returns an [error](https://tofupay.com/docs/api#errors) if update parameters are invalid (e.g. specifying an invalid coupon or an invalid card).








## Delete a customer

> ### DEFINITION
> DELETE https://api.tofupay.com/v1/customers/{CUSTOMER_ID}
> ### Example Request

```shell
curl https://api.tofupay.com/v1/customers/cus_5V50idQJ7fxkRX \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc: \
   -X DELETE
```

```ruby
require "tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

cu = Tofupay::Customer.retrieve("cus_5V50idQJ7fxkRX")
cu.delete
```

```python
import tofupay
tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

cu = tofupay.Customer.retrieve("cus_5V50idQJ7fxkRX")
cu.delete()
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

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
Returns an object with a deleted parameter on success. If the customer ID does not exist, this call returns an [error](https://tofupay.com/docs/api#errors).




