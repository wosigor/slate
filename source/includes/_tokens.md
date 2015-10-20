# Tokens

Often you want to be able to charge credit cards or send payments to bank accounts without having to hold sensitive card information on your own servers. Tofupay.js makes this easy in the browser, but you can use the same technique in other environments with our token API.
Tokens can be created with your publishable API key, which can safely be embedded in downloadable applications like iPhone and Android apps. You can then use a token anywhere in our API that a card or bank account is accepted. Note that tokens are not meant to be stored or used more than once—to store these details for use later, you should create Customer object.

## The token object

> ### Example Response

```json
{
  "id": "tok_uKe9EMELcrJ0fkaw9FBmtsSj",
  "object": "card_token",
  "livemode": false,
  "created_at": 1443078014,
  "card": {
    "id": "card_JFo8SEr7pNHoiJ8jfGrbCGn",
    "object": "card",
    "created_at": 1443078014,
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
  }
}
```

### Parameters

Parameter | Type | Description
--------- | ------- | ----------- | -----------
id | string | The ID of the token.
object |  string | 'token'
livemode | boolean | True - live, False - sandbox
created_at | timestamp | Time of creation
card | dictionary | Dictionary containg a user's card details.
| | | |
card[number] | string | The card number without any spaces.
card[expire_month] | integer | Card expiry month. Format MM
card[expire_year] | string | Card expiry year. Format YY
card[ccv] | string | Card security code.
card[holder_name] | string | Card holder full name.
card[address_1] | string | Registered card address information.
card[address_2] | string |
card[address_city] | string |
card[address_country] | string | Two-letter ISO code representing the country of the card.
card[address_postcode] | string |
card[customer] | string | ID of a customer which the card is attached to.







## Create a card token

> ### Definition
> POST https://sandbox.tofupay.com/v1/tokens
> ### Example Request

```shell
curl https://sandbox.tofupay.com/v1/tokens \
   -u key_private_sandbox_8j48HWFp94UldHpJDzHgDUl: \
   -d card[number]=4242424242424242 \
   -d card[exp_month]=12 \
   -d card[exp_year]=2016 \
   -d card[cvc]=123
```

```ruby
require "Tofupay"
Tofupay.api_key = "key_private_sandbox_8j48HWFp94UldHpJDzHgDUl"

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
Tofupay.api_key = "key_private_sandbox_8j48HWFp94UldHpJDzHgDUl"

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
\Tofupay\Tofupay::setApiKey("key_private_sandbox_8j48HWFp94UldHpJDzHgDUl");

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
  "id": "tok_uKe9EMELcrJ0fkaw9FBmtsSj",
  "object": "card_token",
  "livemode": false,
  "created_at": 1443078014,
  "card": {
    "id": "card_JFo8SEr7pNHoiJ8jfGrbCGn",
    "object": "card",
    "created_at": 1443078014,
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
  }
}
```

Creates a single use token that wraps the details of a credit card. This token can be used in place of a credit card dictionary with any API method. These tokens can only be used once: by creating a new transaction object, or attaching them to a customer.

### Parameters

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
number | **Y** | string | The card number without any spaces.
expire_month | **Y** | integer | Card expiry month. Format MM
expire_year | **Y** | string | Card expiry year. Format YY
| | |
ccv | **Y**  | string | Card security code.
holder_name | **Y**  | string | Card holder full name.
address_1 | **Y**  | string | Registered card address information.
address_2 | N | string |
address_city | **Y**  | string |
address_country | **Y**  | string | Two-letter ISO code representing the country of the card.
address_postcode | N | string |

### Returns
The created card token object is returned if successful. Otherwise, this call returns an error.











## Retrieve a token

> ### Definition
> GET https://sandbox.tofupay.com/v1/tokens/{TOKEN_ID}
> ### Example Request

```ruby
require "Tofupay"
Tofupay.api_key = "key_private_sandbox_8j48HWFp94UldHpJDzHgDUl"

Tofupay::Token.retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn")
```

```python
import Tofupay
Tofupay.api_key = "key_private_sandbox_8j48HWFp94UldHpJDzHgDUl"

Tofupay.Token.retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn")
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_8j48HWFp94UldHpJDzHgDUl");

\Tofupay\Token::retrieve("tok_15XZLsLdZh7jQOUq86ISvtjn");
```

```shell
curl https://sandbox.tofupay.com/v1/tokens/tok_15XZLsLdZh7jQOUq86ISvtjn \
   -u key_private_sandbox_8j48HWFp94UldHpJDzHgDUl:
```

> ### Example Response

```json
{
  "id": "tok_uKe9EMELcrJ0fkaw9FBmtsSj",
  "object": "card_token",
  "livemode": false,
  "created_at": 1443078014,
  "card": {
    "id": "card_JFo8SEr7pNHoiJ8jfGrbCGn",
    "object": "card",
    "created_at": 1443078014,
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
