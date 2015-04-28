# Errors

Tofupay uses conventional HTTP response codes to indicate success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that resulted from the provided information (e.g. a required parameter was missing, a charge failed, etc.), and codes in the 5xx range indicate an error with Tofupay's servers.
Not all errors map cleanly onto HTTP response codes, however. When a request is valid but does not complete successfully (e.g. a card is declined), we return a 402 error code.

The Tofupay API uses the following error codes:


## HTTP status codes

Status Code | Meaning
---------- | -------
400        | Bad Request -- Often missing a required parameter.
401        | Unauthorized -- Your API key is wrong
403        | Forbidden -- The kitten requested is hidden for administrators only
404        | Not Found -- The specified request could not be found
405        | Method Not Allowed -- You tried to access a kitten with an invalid method
500        | Internal Server Error -- We had a problem with our server. Try again later.
503        | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.

## Error types

Error Type | Meaning
---------- | -------
invalid_request_error | Invalid request errors arise when your request has invalid parameters.
api_error | API errors cover any other type of problem (e.g. a temporary problem with Stripe's servers) and should turn up only very infrequently.
card_error | Card errors are the most common type of error you should expect to handle. They result when the user enters a card that can't be charged for some reason.

## Error codes

Error Code | Meaning
---------- | -------
incorrect_number | The card number is incorrect.
invalid_number | The card number is not a valid credit card number.
invalid_expiry_month | The card's expiration month is invalid.
invalid_expiry_year | The card's expiration year is invalid.
invalid_cvc | The card's security code is invalid.
expired_card | The card has expired.
incorrect_cvc | The card's security code is incorrect.
incorrect_zip | The card's zip code failed validation.
card_declined | The card was declined.
missing | There is no card on a customer that is being charged.
processing_error | An error occurred while processing the card.
rate_limit | An error occurred due to requests hitting the API too quickly. Please let us know if you're consistently running into this error.

