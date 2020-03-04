
# API Reference

> To authorize, use this code:


```python
import requests
import json

url = "https://besttime.app/api/v1/"

headers = {
    'Content-Type': 'application/json'
}

payload = json.dumps({
    'api_key_private': 'e267713ecda84c77a055294dbb12c6d4'
})

response = requests.request("POST", url, headers=headers, data = payload)

response_dict = json.loads(response.text.encode('utf8'))
```

```shell
# cURL
curl --location --request POST 'https://besttime.app/api/v1/' \
--header 'Content-Type: application/json' \
--data-raw '{
	"api_key_private": "e267713ecda84c77a055294dbb12c6d4"
}	'
```

```javascript
var settings = {
  "url": "https://besttime.app/api/v1/",
  "method": "POST",
  "headers": {
    "Content-Type": "application/json"
  },
  "data": JSON.stringify({
    "api_key_private":"e267713ecda84c77a055294dbb12c6d4"
    }),
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```


> The above command returns JSON structured like this:

```json
  {
    'status' : 'OK',
    'message' : 'Valid api_key_private',
    'valid': true,
    'quota_forecasts_remaining' : 300,
    'quota_queries_remaining' : 1000000
  }
```

<details>
  <summary>stuff with *mark* **down**</summary>
  <p>
<!-- the above p cannot start right at the beginning of the line and is mandatory for everything else to work -->
##*formatted* **heading** with [a](link)
```java
code block
```

  <details>
    <summary><small>nested</small> stuff</summary><p>
<!-- alternative placement of p shown above -->

* list
* with

 1. nested
 1. items

    ```java
    // including code
    ```
 1. blocks

  </p></details>
</p></details>


BestTime.app uses API keys to allow access to the API. You can find or generate API keys at the [API keys Management](http://besttime.app/api/v1/api_keys_list) page.

BestTime.app expects for the API key to be included in all API requests to the server. 
Our API accepts only JSON-encoded POST request and returns JSON-encoded responses.
This makes it easier to request business names and addresses without encoding them (for example as GET parameters)

<aside class="notice">
Make sure to replace <code>e267713ecda84c77a055294dbb12c6d4</code> with your 32 char API key.
</aside>

## API Keys 

Authentication for the API is done using API keys.

There are two types of API keys. Private keys to create a new forecast, and public keys to query data from existing forecasted businesses. The private key can be used to create, delete and list forecasts. As the name suggests, the private key should be kept secret, in order to avoid other people from forecasting new businesses and abusing your limited forecast credits. The public key can be used to query existing business forecasts. It can only used get existing forecast data (read-only). 

### insert api request with api_key_ examples in json body

API keys are generated in pairs, and you can generate multiple API key sets (pairs) in the API key management page. When using multiple API keys, you should remember that you can only query forecasts from the same key set. 

All key sets use credits from the same account. When an API key is compromised you can delete the API key set through the API Key management page.

## Authentication

<code>api_key_private</code>
<code>api_key_public</code>


## Credits

There are two types of credits. Forecast credits and query credits. 
When forecasting a business using the private API key a 'forecast credit' is substracted from your account. When querying an existing forecast a 'query credit' is substracted from your account. 

Forecast credits are substracted when a forecast is succesfully made and saved on the server. It won't substract a forecast query when:

* The business is not found
* The business is found but it could not be forecasted (when there is not enough data)
* The forecast fails (internal error)

When querying an existing forecast a query credit is subtracted for every request. Each subscription plans contains at least 1000x more query credits than forecast queries. The public API key can only perform read-only actions, but you could choose to hide the public key on public websites (e.g. in your website back-end) to lower your query credit usage (or to prevent abuse).

| Goal                               | Credits used     | API Key required | Parameter       |
|------------------------------------|------------------|------------------|-----------------|
| Create a new forecast              | Forecast credits | Private          | api_key_private |
| Get live data (platiunum only)     | Forecast credits | Private          | api_key_private |
| List all forecast by business_id   | None             | Private          | api_key_private |
| Query data from existing forecasts | Query credits    | Public           | api_key_public  |

### Subscription plans
Credits will be added at the start of every monthly invoice cycle, when you upgrade, or when you buy extra credit bundles (only for selected subscription plans). Credits don't expire and automatically roll over to the next month.