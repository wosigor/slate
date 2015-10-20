---
title: API Reference

language_tabs:
  - shell: cURL
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - javascript: Node
  - go: Go

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - tokens
  - transactions
  - customers
  - cards
  - errors

search: true
---

# Introduction

> ### API Endpoint
> https://api.tofupay.com

### API Reference

The Tofupay API is organized around [REST](http://en.wikipedia.org/wiki/Representational_state_transfer). Our API is designed to have predictable, resource-oriented URLs and to use HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which can be understood by off-the-shelf HTTP clients, and we support [cross-origin resource sharing](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) to allow you to interact securely with our API from a client-side web application (though you should remember that you should never expose your secret API key in any public website's client-side code). [JSON](http://www.json.org/) will be returned in all responses from the API, including errors (though if you're using API bindings, we will convert the response to the appropriate language-specific object).
To make the Tofupay API as explorable as possible, accounts have test-mode API keys as well as live-mode API keys. These keys can be active at the same time. Data created with test-mode credentials will never hit the credit card networks and will never cost anyone money.











# Authentication

> ### Example Request

```shell
curl https://api.tofupay.com/v1/transactions \
   -u key_private_sandbox_8j48HWFp94UldHpJDzHgDUl:
```

> curl uses the -u flag to pass basic auth credentials (adding a colon after your API key will prevent it from asking you for a password).


```ruby
require "tofupay"
Tofupay.api_key = "key_private_sandbox_8j48HWFp94UldHpJDzHgDUl"
```

```python
import tofupay
tofupay.api_key = "key_private_sandbox_8j48HWFp94UldHpJDzHgDUl"
```

```php
\Tofupay\Tofupay::setApiKey("key_private_sandbox_8j48HWFp94UldHpJDzHgDUl");
```

> The API key has been preset for you.

You authenticate to the Tofupay API by providing one of your API keys in the request. You can manage your API keys from your [account](https://dashboard-staging.tofupay.com). You can have multiple API keys active at one time. Your API keys carry many privileges, so be sure to keep them secret!
To use your API key, you need only set tofupay.api_key equal to the key. 
All API requests must be made over [HTTPS](http://en.wikipedia.org/wiki/HTTPS). Calls made over plain HTTP will fail. You must authenticate for all requests.

`Authorization: api.key`

<aside class="notice">
You must replace `api.key` with your personal API key.
</aside>
