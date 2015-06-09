# Tokens

Often you want to be able to charge credit cards or send payments to bank accounts without having to hold sensitive card information on your own servers. Tofupay.js makes this easy in the browser, but you can use the same technique in other environments with our token API.
Tokens can be created with your publishable API key, which can safely be embedded in downloadable applications like iPhone and Android apps. You can then use a token anywhere in our API that a card or bank account is accepted. Note that tokens are not meant to be stored or used more than once—to store these details for use later, you should create Customer or Recipient objects.

## The token object

> ### Example Response

```json
{
  "id": "tok_5yNys5VrM2Te8XY-3fiGh5Pw",
  "object": "card_token",
  "livemode": false,
  "created_at": 1433855669,
  "card": {
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
  }
}
```

### Parameters

Parameter | Type | Description
--------- | ------- | ----------- | -----------
id | string | The ID of the token.
object |  string | 'token'
created_at | timestamp | Time of creation
livemode | boolean | True - live, False - sandbox








## Create a card token

> ### Definition
> POST https://api.tofupay.com/v1/tokens
> ### Example Request

```shell
curl https://api.Tofupay.com/v1/tokens \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc: \
   -d card[number]=4242424242424242 \
   -d card[exp_month]=12 \
   -d card[exp_year]=2016 \
   -d card[cvc]=123
```

```ruby
require "Tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay::Token.create(
  :card => {
    :number => "4242424242424242",
    :exp_month => 4,
    :exp_year => 2016,
    :cvc => "314"
  },
)
```

```python
import Tofupay
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

tofupay.Token.create(
  card={
    "number": '4242424242424242',
    "exp_month": 12,
    "exp_year": 2016,
    "cvc": '123'
  },
)
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

\Tofupay\Token::create(array(
  "card" => array(
    "number" => "4242424242424242",
    "exp_month" => 4,
    "exp_year" => 2016,
    "cvc" => "314"
  )
));
```

> ### Example Response

```json
{
  "id": "tok_pyPkf6WFrHY7A97ZEBWdqUKs",
  "created_at": 1430200302,
  "card": {
    "id": "card_uT8mw0wgSwDtSx3WzpyqGqOI",
    "object": "card",
    "brand": null,
    "last_four": 4242,
    "expire_month": 5,
    "expire_year": 2016,
    "holder_name": "Tofu Pay",
    "country": "HK",
    "address_1": null,
    "address_2": null,
    "address_city": null,
    "address_country": null,
    "address_postcode": null
  }
}
```

Creates a single use token that wraps the details of a credit card. This token can be used in place of a credit card dictionary with any API method. These tokens can only be used once: by creating a new charge object, or attaching them to a customer.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
number | **Y** | string | The card number without any spaces.
expire_month | **Y** | integer | Card expiry month. Format MM
expire_year | **Y** | string | Card expiry year. Format YY
| | |
ccv | N | string | Card security code.
country | N | string | Two-letter ISO code representing the country of the card. 
holder_name | N | string | Card holder full name.
address_1 | N | string | Registered card address information.
address_2 | N | string |
address_city | N | string |
address_country | N | string | Two-letter ISO code representing the country of the card.
address_postcode | N | string |

### Returns
The created card token object is returned if successful. Otherwise, this call returns an error.











## Retrieve a token

> ### Definition
> GET https://api.tofupay.com/v1/tokens/{TOKEN_ID}
> ### Example Request

```ruby
require "Tofupay"
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay::Token.retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn")
```

```python
import Tofupay
Tofupay.api_key = "sk_test_qg15eqpUrbT6Gufhjq9ds0Jc"

Tofupay.Token.retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn")
```

```php
\Tofupay\Tofupay::setApiKey("sk_test_qg15eqpUrbT6Gufhjq9ds0Jc");

\Tofupay\Token::retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn");
```

```shell
curl https://api.tofupay.com/v1/tokens/tok_15XZLsLdZh7jQOUq86ISvtjn \
   -u sk_test_qg15eqpUrbT6Gufhjq9ds0Jc:
```

> ### Example Response

```json
{
  "id": "tok_pyPkf6WFrHY7A97ZEBWdqUKs",
  "created_at": 1430200302,
  "card": {
    "id": "card_uT8mw0wgSwDtSx3WzpyqGqOI",
    "object": "card",
    "brand": null,
    "last_four": 4242,
    "expire_month": 5,
    "expire_year": 2016,
    "holder_name": "Tofu Pay",
    "country": "HK",
    "address_1": null,
    "address_2": null,
    "address_city": null,
    "address_country": null,
    "address_postcode": null
  }
}
```

Retrieves the token with the given ID.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
id | Y | string | The ID of the desired token.

### Returns
Returns a token if a valid ID was provided. Raises an error otherwise.
