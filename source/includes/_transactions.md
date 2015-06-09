# Transactions

To transaction a credit or a debit card, you create a transaction object. You can retrieve and refund individual transactions as well as list all transactions. Transactions are identified by a unique random ID.

## The transaction object

> ### Example Response

```json
{
  "id": "txn_15r6GrLdZh7jQOUqvvc9t1fA",
  "object": "transaction",
  "created": 1428926553,
  "livemode": false,
  "paid": true,
  "status": "succeeded",
  "amount": 1000,
  "currency": "usd",
  "refunded": false,
  "token": {
    "id": "card_15r6GqLdZh7jQOUqtMqEPMu2",
    "object": "card",
    "last4": "4242",
    "brand": "Visa",
    "funding": "credit",
    "exp_month": 4,
    "exp_year": 2016,
    "country": "US",
    "name": null,
    "address_line1": null,
    "address_line2": null,
    "address_city": null,
    "address_state": null,
    "address_zip": null,
    "address_country": null,
    "cvc_check": null,
    "address_line1_check": null,
    "address_zip_check": null,
    "dynamic_last4": null,
    "metadata": {
    },
    "customer": null
  },
  "captured": true,
  "balance_transaction": "txn_15IehrLdZh7jQOUq2dX5hcyV",
  "failure_message": null,
  "failure_code": null,
  "amount_refunded": 0,
  "customer": null,
  "invoice": null,
  "description": "",
  "dispute": null,
  "metadata": {
  },
  "statement_descriptor": null,
  "fraud_details": {
  },
  "receipt_email": null,
  "receipt_number": null,
  "shipping": null,
  "application_fee": null,
  "refunds": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/transactions/txn_15r6GrLdZh7jQOUqvvc9t1fA/refunds",
    "data": [

    ]
  }
}
```

### Parameters

Parameter | Type | Description
--------- | ------- | ----------- | -----------
id | string | The ID of the desired transaction.
object |  string | 'transaction'
created | timestamp | 
| |









## Create a transaction

> ### DEFINITION
> POST https://api.tofupay.com/v1/transactions
> ### Example Request

```shell
curl https://api.tofupay.com/v1/transactions \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc: \
   -d amount=400 \
   -d currency=usd \
   -d token=tok_15XZLsLdZh7jQOUq86ISvtjn \
   -d description="Transaction for test@example.com"
```

```ruby
require "tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay::Transaction.create(
  :amount => 400,
  :currency => "usd",
  :token => "tok_15XZLsLdZh7jQOUq86ISvtjn", # obtained with Tofupay.js
  :description => "Transaction for test@example.com"
)
```

```python
import tofupay
tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

tofupay.Transaction.create(
  amount=400,
  currency="usd",
  token="tok_15XZLsLdZh7jQOUq86ISvtjn", # obtained with Tofupay.js
  description="Transaction for test@example.com"
)
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

\Tofupay\Transaction::create(array(
  "amount" => 400,
  "currency" => "usd",
  "token" => "tok_15XZLsLdZh7jQOUq86ISvtjn", // obtained with Tofupay.js
  "description" => "Transaction for test@example.com"
));
```

> ### Example Response

```json
{
  "id": "txn_15r6GrLdZh7jQOUqvvc9t1fA",
  "object": "transaction",
  "created": 1428926553,
  "livemode": false,
  "paid": true,
  "status": "succeeded",
  "amount": 1000,
  "currency": "usd",
  "refunded": false,
  "token": {
    "id": "card_15r6GqLdZh7jQOUqtMqEPMu2",
    "object": "card",
    "last4": "4242",
    "brand": "Visa",
    "funding": "credit",
    "exp_month": 4,
    "exp_year": 2016,
    "country": "US",
    "name": null,
    "address_line1": null,
    "address_line2": null,
    "address_city": null,
    "address_state": null,
    "address_zip": null,
    "address_country": null,
    "cvc_check": null,
    "address_line1_check": null,
    "address_zip_check": null,
    "dynamic_last4": null,
    "metadata": {
    },
    "customer": null
  },
  "captured": true,
  "balance_transaction": "txn_15IehrLdZh7jQOUq2dX5hcyV",
  "failure_message": null,
  "failure_code": null,
  "amount_refunded": 0,
  "customer": null,
  "invoice": null,
  "description": "",
  "dispute": null,
  "metadata": {
  },
  "statement_descriptor": null,
  "fraud_details": {
  },
  "receipt_email": null,
  "receipt_number": null,
  "shipping": null,
  "application_fee": null,
  "refunds": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/transactions/txn_15r6GrLdZh7jQOUqvvc9t1fA/refunds",
    "data": [

    ]
  }
}
```

To transaction a credit card, you create a transaction object. If your API key is in test mode, the supplied card won't actually be transactiond, though everything else will occur as if in live mode. (tofupay assumes that the transaction would have completed successfully).

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
amount | **Y** | double | The amount to be transactiond.
currency | **Y** | string | 3-letter [ISO code](https://support.tofupay.com/questions/which-currencies-does-tofupay-support) for currency.
token | optional, either **token** or **customer** is required | string | A payment card token.
| | |
customer | optional, either **token** or **customer** is required | string | An ID of a customer to be transactiond.
country | N | string | Two-letter ISO code representing the country of the card. 
description | N | string | Additional optional description of the transaction.
capture | N, default **true** | boolean | Whether or not to immediately capture the transaction. When false, the transaction issues an authorization (or pre-authorization), and will need to be captured later. Uncaptured transactions expire in 7 days. For more information, see authorizing 

### Returns
Returns a transaction object if the transaction succeeded. Returns an [error](https://tofupay.com/docs/api#errors) if something goes wrong. A common source of error is an invalid or expired card, or a valid card with insufficient available balance.












## Retrieve a transaction

> ### DEFINITION
> GET https://api.tofupay.com/v1/transactions/{TRANSACTION_ID}
> ### Example Request

```shell
curl https://api.tofupay.com/v1/transactions/tok_15XZLsLdZh7jQOUq86ISvtjn \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc:
```

```ruby
require "Tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay::Transaction.retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn")
```

```python
import Tofupay
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay.Transaction.retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn")
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

\Tofupay\Transaction::retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn");
```
> ### Example Response

```json
{
  "id": "txn_15r6GrLdZh7jQOUqvvc9t1fA",
  "object": "transaction",
  "created": 1428926553,
  "livemode": false,
  "paid": true,
  "status": "succeeded",
  "amount": 1000,
  "currency": "usd",
  "refunded": false,
  "token": {
    "id": "card_15r6GqLdZh7jQOUqtMqEPMu2",
    "object": "card",
    "last4": "4242",
    "brand": "Visa",
    "funding": "credit",
    "exp_month": 4,
    "exp_year": 2016,
    "country": "US",
    "name": null,
    "address_line1": null,
    "address_line2": null,
    "address_city": null,
    "address_state": null,
    "address_zip": null,
    "address_country": null,
    "cvc_check": null,
    "address_line1_check": null,
    "address_zip_check": null,
    "dynamic_last4": null,
    "metadata": {
    },
    "customer": null
  },
  "captured": true,
  "balance_transaction": "txn_15IehrLdZh7jQOUq2dX5hcyV",
  "failure_message": null,
  "failure_code": null,
  "amount_refunded": 0,
  "customer": null,
  "invoice": null,
  "description": "",
  "dispute": null,
  "metadata": {
  },
  "statement_descriptor": null,
  "fraud_details": {
  },
  "receipt_email": null,
  "receipt_number": null,
  "shipping": null,
  "application_fee": null,
  "refunds": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/transactions/txn_15r6GrLdZh7jQOUqvvc9t1fA/refunds",
    "data": [

    ]
  }
}
```

Retrieves the transactions object if a valid identifier was provided, and returns an [error](https://tofupay.com/docs/api#errors) otherwise.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
id | Y | string | The ID of the desired transaction.

### Returns
Returns a transaction if a valid ID was provided. Raises an error otherwise.














## Retrieve all transactions

> ### DEFINITION
> GET https://api.tofupay.com/v1/transactions
> ### Example Request

```shell
curl https://api.tofupay.com/v1/transactions?limit=3 \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc:
```

```ruby
require "Tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay::Transaction.all(:limit => 3)
```

```python
import Tofupay
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay.Transaction.all(limit=3)
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

\Tofupay\Transaction::all(array("limit" => 3));
```

> ### Example Response

```json
{
  "object": "list",
  "url": "/v1/transactions",
  "has_more": false,
  "data": [
    {
      "id": "txn_15r6GrLdZh7jQOUqvvc9t1fA",
      "object": "transaction",
      "created": 1428926553,
      "livemode": false,
      "paid": true,
      "status": "succeeded",
      "amount": 1000,
      "currency": "usd",
      "refunded": false,
      "source": {
        "id": "card_15r6GqLdZh7jQOUqtMqEPMu2",
        "object": "card",
        "last4": "4242",
        "brand": "Visa",
        "funding": "credit",
        "exp_month": 4,
        "exp_year": 2016,
        "country": "US",
        "name": null,
        "address_line1": null,
        "address_line2": null,
        "address_city": null,
        "address_state": null,
        "address_zip": null,
        "address_country": null,
        "cvc_check": null,
        "address_line1_check": null,
        "address_zip_check": null,
        "dynamic_last4": null,
        "metadata": {
        },
        "customer": null
      },
      "captured": true,
      "balance_transaction": "txn_15IehrLdZh7jQOUq2dX5hcyV",
      "failure_message": null,
      "failure_code": null,
      "amount_refunded": 0,
      "customer": null,
      "invoice": null,
      "description": "",
      "dispute": null,
      "metadata": {
      },
      "statement_descriptor": null,
      "fraud_details": {
      },
      "receipt_email": null,
      "receipt_number": null,
      "shipping": null,
      "application_fee": null,
      "refunds": {
        "object": "list",
        "total_count": 0,
        "has_more": false,
        "url": "/v1/transactions/txn_15r6GrLdZh7jQOUqvvc9t1fA/refunds",
        "data": [
    
        ]
      }
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








## Update a transaction

> ### DEFINITION
> POST https://api.tofupay.com/v1/transaction/{TRANSACTION_ID}
> ### Example Request

```shell
curl https://api.tofupay.com/v1/transactions/txn_15r6GrLdZh7jQOUqvvc9t1fA \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc: \
   -d description="Transaction for test@example.com"
```

```ruby
require "tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

ch = Tofupay::Charge.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.description = "Charge for test@example.com"
ch.save
```

```python
import tofupay
tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

ch = tofupay.Charge.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.description = "Charge for test@example.com"
ch.save()
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

$ch = \Tofupay\Charge::retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA");
$ch->description = "Charge for test@example.com";
$ch->save();
```
> ### Example Response

```json
{
  "id": "txn_15r6GrLdZh7jQOUqvvc9t1fA",
  "object": "transaction",
  "created": 1428926553,
  "livemode": false,
  "paid": true,
  "status": "succeeded",
  "amount": 1000,
  "currency": "usd",
  "refunded": false,
  "token": {
    "id": "card_15r6GqLdZh7jQOUqtMqEPMu2",
    "object": "card",
    "last4": "4242",
    "brand": "Visa",
    "funding": "credit",
    "exp_month": 4,
    "exp_year": 2016,
    "country": "US",
    "name": null,
    "address_line1": null,
    "address_line2": null,
    "address_city": null,
    "address_state": null,
    "address_zip": null,
    "address_country": null,
    "cvc_check": null,
    "address_line1_check": null,
    "address_zip_check": null,
    "dynamic_last4": null,
    "metadata": {
    },
    "customer": null
  },
  "captured": true,
  "balance_transaction": "txn_15IehrLdZh7jQOUq2dX5hcyV",
  "failure_message": null,
  "failure_code": null,
  "amount_refunded": 0,
  "customer": null,
  "invoice": null,
  "description": "",
  "dispute": null,
  "metadata": {
  },
  "statement_descriptor": null,
  "fraud_details": {
  },
  "receipt_email": null,
  "receipt_number": null,
  "shipping": null,
  "application_fee": null,
  "refunds": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/transactions/txn_15r6GrLdZh7jQOUqvvc9t1fA/refunds",
    "data": [

    ]
  }
}
```

Updates the specified transaction by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
description | N | string | The description of the transaction.

### Returns
Returns the transaction object if the update succeeded. This call will return an [error](https://tofupay.com/docs/api#errors) if update parameters are invalid.












## Capture a transaction

> ### DEFINITION
> POST https://api.tofupay.com/v1/transactions/{TRANSACTION_ID}/capture
> ### Example Request

```shell
curl https://api.tofupay.com/v1/transactions/tok_15XZLsLdZh7jQOUq86ISvtjn/capture \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc: \
   -X POST
```

```ruby
require "tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

ch = Tofupay::transaction.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.capture
```

```python
import tofupay
tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

ch = tofupay.transaction.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.capture()
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

$ch = \Tofupay\transaction::retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA");
$ch->capture();
```

> ### Example Response

```json
{
  "id": "txn_15r6GrLdZh7jQOUqvvc9t1fA",
  "object": "transaction",
  "created": 1428926553,
  "livemode": false,
  "paid": true,
  "status": "succeeded",
  "amount": 1000,
  "currency": "usd",
  "refunded": false,
  "source": {
    "id": "card_15r6GqLdZh7jQOUqtMqEPMu2",
    "object": "card",
    "last4": "4242",
    "brand": "Visa",
    "funding": "credit",
    "exp_month": 4,
    "exp_year": 2016,
    "country": "US",
    "name": null,
    "address_line1": null,
    "address_line2": null,
    "address_city": null,
    "address_state": null,
    "address_zip": null,
    "address_country": null,
    "cvc_check": null,
    "address_line1_check": null,
    "address_zip_check": null,
    "dynamic_last4": null,
    "metadata": {
    },
    "customer": null
  },
  "captured": true,
  "balance_transaction": "txn_15IehrLdZh7jQOUq2dX5hcyV",
  "failure_message": null,
  "failure_code": null,
  "amount_refunded": 0,
  "customer": null,
  "invoice": null,
  "description": "",
  "dispute": null,
  "metadata": {
  },
  "statement_descriptor": null,
  "fraud_details": {
  },
  "receipt_email": null,
  "receipt_number": null,
  "shipping": null,
  "application_fee": null,
  "refunds": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/transactions/txn_15r6GrLdZh7jQOUqvvc9t1fA/refunds",
    "data": [

    ]
  }
}
```

Capture the payment of an existing, uncaptured, transaction. This is the second half of the two-step payment flow, where first you [created a transaction](https://tofupay.com/docs/api/curl#create_transaction) with the capture option set to false.
Uncaptured payments expire exactly seven days after they are created. If they are not captured by that point in time, they will be marked as refunded and will no longer be capturable.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
id | Y | string | The ID of the desired transaction.

### Returns
Returns the transaction object, with an updated captured property (set to true). Capturing a transaction will always succeed, unless the transaction is already refunded, expired, captured, or an invalid capture amount is specified, in which case this method will return an [error](https://tofupay.com/docs/api#errors).







## Refund a transaction

> ### DEFINITION
> POST https://api.tofupay.com/v1/transactions/{TRANSACTION_ID}/refund
> ### Example Request

```shell
curl https://api.tofupay.com/v1/transactions/tok_15XZLsLdZh7jQOUq86ISvtjn/refunds \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc: \
   -X POST
```

```ruby
require "tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

ch = Tofupay::transaction.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.refund
```

```python
import tofupay
tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

ch = tofupay.transaction.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.refund()
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

$ch = \Tofupay\transaction::retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA");
$ch->refund();
```

> ### Example Response

```json
{
  "id": "txn_15r6GrLdZh7jQOUqvvc9t1fA",
  "object": "transaction",
  "created": 1428926553,
  "livemode": false,
  "paid": true,
  "status": "succeeded",
  "amount": 1000,
  "currency": "usd",
  "refunded": true,
  "source": {
    "id": "card_15r6GqLdZh7jQOUqtMqEPMu2",
    "object": "card",
    "last4": "4242",
    "brand": "Visa",
    "funding": "credit",
    "exp_month": 4,
    "exp_year": 2016,
    "country": "US",
    "name": null,
    "address_line1": null,
    "address_line2": null,
    "address_city": null,
    "address_state": null,
    "address_zip": null,
    "address_country": null,
    "cvc_check": null,
    "address_line1_check": null,
    "address_zip_check": null,
    "dynamic_last4": null,
    "metadata": {
    },
    "customer": null
  },
  "captured": true,
  "balance_transaction": "txn_15IehrLdZh7jQOUq2dX5hcyV",
  "failure_message": null,
  "failure_code": null,
  "amount_refunded": 0,
  "customer": null,
  "invoice": null,
  "description": "",
  "dispute": null,
  "metadata": {
  },
  "statement_descriptor": null,
  "fraud_details": {
  },
  "receipt_email": null,
  "receipt_number": null,
  "shipping": null,
  "application_fee": null,
  "refunds": {
    "object": "list",
    "total_count": 0,
    "has_more": false,
    "url": "/v1/transactions/txn_15r6GrLdZh7jQOUqvvc9t1fA/refunds",
    "data": [

    ]
  }
}
```

Creating a new refund will refund a transaction that has previously been created but not yet refunded. Funds will be refunded to the credit or debit card that was originally charged. The fees you were originally charged are also refunded.

Once entirely refunded, a charge can't be refunded again. This method will return an error when called on an already-refunded transaction, or when trying to refund more money than is left on a transaction.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
amount | N | double | The amount represneting how much of this transaction to refund.

### Returns
Returns the transaction object, with an updated refund property (set to true). Refunding a transaction will always succeed, unless the transaction is already refunded, expired, or an invalid refund amount is specified, in which case this method will return an [error](https://tofupay.com/docs/api#errors).



