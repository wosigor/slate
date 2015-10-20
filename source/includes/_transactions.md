# Transactions

To transaction a credit or a debit card, you create a transaction object. You can retrieve and refund individual transactions as well as list all transactions. Transactions are identified by a unique random ID.

## The transaction object

> ### Example Response

```json
{
  "id": "txn_7jxk6UZWzPI0MAvjOdIVFs",
  "object": "transaction",
  "livemode": false,
  "created_at": 1443080242,
  "paid": false,
  "status": "succeded",
  "amount": 2000,
  "currency": "usd",
  "captured": true,
  "refunded": false,
  "payment_method": {
    "id": "card_Re4tQzKBEPm4586TcgLCCnbt",
    "object": "card",
    "created_at": 1443079778,
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
    "customer": null
  },
  "failure_message": null,
  "failure_code": null,
  "amount_refunded": 0,
  "refunds": {
    "object": "list",
    "url": "/v1/transactions/txn_7jxk6UZWzPI0MAvjOdIVFs/refunds",
    "data": []
  }
}
```

### Parameters

Parameter | Type | Description
--------- | ------- | ----------- | -----------
id | string | The ID of the desired transaction.
object |  string | 'transaction'
created_at | timestamp | Time of creation
livemode | boolean | True - live, False - sandbox
paid | boolean | True - if transaction succeed.
status | string | Status of payment - succeded or failed.
amount | integer | The amount to be transactiond.
currency | string | 3-letter [ISO code](https://support.tofupay.com/questions/which-currencies-does-tofupay-support) for currency.
payment_method | string | A payment card token.
| | |
customer | string | An ID of a customer this transaction is for (if exists).
country | string | Two-letter ISO code representing the country of the card. 
description | string | Additional optional description of the transaction.
captured | boolean | Whether or not to immediately capture the transaction. When false, the transaction issues an authorization (or pre-authorization), and will need to be captured later. Uncaptured transactions expire in 7 days. For more information, see authorizing
refunded | boolean | True if tranaction is fully refunded
failure_message | string | Description of the failure if transaction failed.
failure_code | string | Code of the failure.
amount_refunded | integer | Total amount of the refunded transaction.
refunds | list | List of refunds attached to transaction.










## Create a transaction

> ### DEFINITION
> POST https://sandbox.tofupay.com/v1/transactions
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/transactions \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT: \
   -d amount=400 \
   -d currency=usd \
   -d token=tok_15XZLsLdZh7jQOUq86ISvtjn \
   -d description="Transaction for test@example.com"
```

```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

Tofupay::Transaction.create(
  :amount => 400,
  :currency => "usd",
  :token => "tok_15XZLsLdZh7jQOUq86ISvtjn", # obtained with Tofupay.js
  :description => "Transaction for test@example.com"
)
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

tofupay.Transaction.create(
  amount=400,
  currency="usd",
  token="tok_15XZLsLdZh7jQOUq86ISvtjn", # obtained with Tofupay.js
  description="Transaction for test@example.com"
)
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

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
  "id": "txn_Fo_kuLTTrA10Sl1xLl2O7BvB",
  "object": "transaction",
  "livemode": false,
  "created_at": 1433855556,
  "amount": "15.99",
  "currency": "hkd",
  "captured": true,
  "paid": false,
  "refunded": false,
  "payment_method": {
    "id": "card_QWmaK4T3LFGvtqu9Xb8uou_l",
    "object": "card",
    "created_at": 1433855537,
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
    "customer": null
  },
  "amount_refunded": "0.0",
  "refunds": {
    "object": "list",
    "count": 0,
    "data": [ ]
  }
}
```

To transaction a credit card, you create a transaction object. If your API key is in test mode, the supplied card won't actually be transactiond, though everything else will occur as if in live mode. (tofupay assumes that the transaction would have completed successfully).

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
amount | **Y** | double | The amount to be transactiond.
currency | **Y** | string | 3-letter [ISO code](https://support.tofupay.com/questions/which-currencies-does-tofupay-support) for currency.
payment_method | optional, either **payment_method** or **customer** is required | string | A payment card token.
| | |
customer | optional, either **payment_method** or **customer** is required | string | An ID of a customer to be transactiond.
country | N | string | Two-letter ISO code representing the country of the card. 
description | N | string | Additional optional description of the transaction.
capture | N, default **true** | boolean | Whether or not to immediately capture the transaction. When false, the transaction issues an authorization (or pre-authorization), and will need to be captured later. Uncaptured transactions expire in 7 days. For more information, see authorizing 

### Returns
Returns a transaction object if the transaction succeeded. Returns an [error](http://wosigor.github.io/slate/#errors) if something goes wrong. A common source of error is an invalid or expired card, or a valid card with insufficient available balance.












## Retrieve a transaction

> ### DEFINITION
> GET https://sandbox.tofupay.com/v1/transactions/{TRANSACTION_ID}
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/transactions/tok_15XZLsLdZh7jQOUq86ISvtjn \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT:
```

```ruby
require "Tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

Tofupay::Transaction.retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn")
```

```python
import Tofupay
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

Tofupay.Transaction.retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn")
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

\Tofupay\Transaction::retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn");
```
> ### Example Response

```json
{
  "id": "txn_Fo_kuLTTrA10Sl1xLl2O7BvB",
  "object": "transaction",
  "livemode": false,
  "created_at": 1433855556,
  "amount": "15.99",
  "currency": "hkd",
  "captured": true,
  "paid": false,
  "refunded": false,
  "payment_method": {
    "id": "card_QWmaK4T3LFGvtqu9Xb8uou_l",
    "object": "card",
    "created_at": 1433855537,
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
    "customer": null
  },
  "amount_refunded": "0.0",
  "refunds": {
    "object": "list",
    "count": 0,
    "data": [ ]
  }
}
```

Retrieves the transactions object if a valid identifier was provided, and returns an [error](http://wosigor.github.io/slate/#errors) otherwise.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
id | Y | string | The ID of the desired transaction.

### Returns
Returns a transaction if a valid ID was provided. Raises an error otherwise.














## Retrieve all transactions

> ### DEFINITION
> GET https://sandbox.tofupay.com/v1/transactions
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/transactions?limit=3 \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT:
```

```ruby
require "Tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

Tofupay::Transaction.all(:limit => 3)
```

```python
import Tofupay
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

Tofupay.Transaction.all(limit=3)
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

\Tofupay\Transaction::all(array("limit" => 3));
```

> ### Example Response

```json
{
  "object": "list",
  "data": [
    {
      "id": "txn_Fo_kuLTTrA10Sl1xLl2O7BvB",
      "object": "transaction",
      "livemode": false,
      "created_at": 1433855556,
      "amount": "15.99",
      "currency": "hkd",
      "captured": true,
      "paid": false,
      "refunded": false,
      "payment_method": {
      "id": "card_QWmaK4T3LFGvtqu9Xb8uou_l",
      "object": "card",
      "created_at": 1433855537,
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
      "customer": null
      },
      "amount_refunded": "0.0",
      "refunds": {
        "object": "list",
        "count": 0,
        "data": [ ]
      }
    },
    {
      "id": "txn_lDIXWSGPOW3VVKTcAKe6_pBE",
      "object": "transaction",
      "livemode": false,
      "created_at": 1433855855,
      "amount": "15.99",
      "currency": "hkd",
      "captured": true,
      "paid": false,
      "refunded": true,
      "payment_method": {
      "id": "card_0sBsD2dkUwTX6vibbOqaf00J",
      "object": "card",
      "created_at": 1433855669,
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
      "customer": null
      },
      "amount_refunded": "15.99",
      "refunds": {
        "object": "list",
        "count": 1,
        "data": [
          {
            "id": "rfnd_bVtaLU_88P3DZIfWTxsTWJas",
            "object": "refund",
            "livemode": false,
            "created_at": 1433855864,
            "amount": "15.99",
            "currency": "hkd",
            "transaction": "txn_lDIXWSGPOW3VVKTcAKe6_pBE",
            "reason": null
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








## Update a transaction

> ### DEFINITION
> POST https://sandbox.tofupay.com/v1/transactions/{TRANSACTION_ID}
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/transactions/txn_15r6GrLdZh7jQOUqvvc9t1fA \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT: \
   -d description="Transaction for test@example.com"
```

```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

ch = Tofupay::Charge.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.description = "Charge for test@example.com"
ch.save
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

ch = tofupay.Charge.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.description = "Charge for test@example.com"
ch.save()
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

$ch = \Tofupay\Charge::retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA");
$ch->description = "Charge for test@example.com";
$ch->save();
```
> ### Example Response

```json
{
  "id": "txn_Fo_kuLTTrA10Sl1xLl2O7BvB",
  "object": "transaction",
  "livemode": false,
  "created_at": 1433855556,
  "amount": "15.99",
  "currency": "hkd",
  "captured": true,
  "paid": false,
  "refunded": false,
  "payment_method": {
    "id": "card_QWmaK4T3LFGvtqu9Xb8uou_l",
    "object": "card",
    "created_at": 1433855537,
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
    "customer": null
  },
  "amount_refunded": "0.0",
  "refunds": {
    "object": "list",
    "count": 0,
    "data": [ ]
  }
}
```

Updates the specified transaction by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
description | N | string | Description of the transaction.

### Returns
Returns the transaction object if the update succeeded. This call will return an [error](http://wosigor.github.io/slate/#errors) if update parameters are invalid.












## Capture a transaction

> ### DEFINITION
> POST https://sandbox.tofupay.com/v1/transactions/{TRANSACTION_ID}/capture
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/transactions/tok_15XZLsLdZh7jQOUq86ISvtjn/capture \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT: \
   -X POST
```

```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

ch = Tofupay::transaction.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.capture
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

ch = tofupay.transaction.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.capture()
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

$ch = \Tofupay\transaction::retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA");
$ch->capture();
```

> ### Example Response

```json
{
  "id": "txn_Fo_kuLTTrA10Sl1xLl2O7BvB",
  "object": "transaction",
  "livemode": false,
  "created_at": 1433855556,
  "amount": "15.99",
  "currency": "hkd",
  "captured": true,
  "paid": false,
  "refunded": false,
  "payment_method": {
    "id": "card_QWmaK4T3LFGvtqu9Xb8uou_l",
    "object": "card",
    "created_at": 1433855537,
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
    "customer": null
  },
  "amount_refunded": "0.0",
  "refunds": {
    "object": "list",
    "count": 0,
    "data": [ ]
  }
}
```

Capture the payment of an existing, uncaptured, transaction. This is the second half of the two-step payment flow, where first you [created a transaction](http://wosigor.github.io/slate//curl#create_transaction) with the capture option set to false.
Uncaptured payments expire exactly seven days after they are created. If they are not captured by that point in time, they will be marked as refunded and will no longer be capturable.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
id | Y | string | The ID of the desired transaction.

### Returns
Returns the transaction object, with an updated captured property (set to true). Capturing a transaction will always succeed, unless the transaction is already refunded, expired, captured, or an invalid capture amount is specified, in which case this method will return an [error](http://wosigor.github.io/slate/#errors).







## Refund a transaction

> ### DEFINITION
> POST https://sandbox.tofupay.com/v1/transactions/{TRANSACTION_ID}/refunds
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/transactions/tok_15XZLsLdZh7jQOUq86ISvtjn/refunds \
   -u key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT: \
   -X POST
```

```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

ch = Tofupay::transaction.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.refund
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT"

ch = tofupay.transaction.retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA")
ch.refund()
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_HUawJJEfQWfgmoaHnfR2tRQT");

$ch = \Tofupay\transaction::retrieve("txn_15r6GrLdZh7jQOUqvvc9t1fA");
$ch->refund();
```

> ### Example Response

```json
{
  "id": "rfnd_bVtaLU_88P3DZIfWTxsTWJas",
  "object": "refund",
  "livemode": false,
  "created_at": 1433855864,
  "amount": "15.99",
  "currency": "hkd",
  "transaction": "txn_lDIXWSGPOW3VVKTcAKe6_pBE",
  "reason": null
}
```

Creating a new refund will refund a transaction that has previously been created but not yet refunded. Funds will be refunded to the credit or debit card that was originally charged. The fees you were originally charged are also refunded.

Once entirely refunded, a charge can't be refunded again. This method will return an error when called on an already-refunded transaction, or when trying to refund more money than is left on a transaction.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
amount | N | double | The amount representing how much of this transaction to refund.
description | N | string | 

### Returns
Returns the transaction object, with an updated refund property (set to true). Refunding a transaction will always succeed, unless the transaction is already refunded, expired, or an invalid refund amount is specified, in which case this method will return an [error](http://wosigor.github.io/slate/#errors).



