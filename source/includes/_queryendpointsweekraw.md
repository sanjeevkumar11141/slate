## Query week raw

> Query the raw week data:

```python
import requests
import json

url = "https://besttime.app/api/v1/forecasts/week/raw"

params = {
    'api_key_public': 'pub_e11661721b084d36b8f469a2c012e754',
    'venue_id': 'ven_51387131543761435650505241346a394a6432395362654a496843',
}

response = requests.request("GET", url, params=params)

data = json.loads(response.text)

print(data)
```

```shell
# cURL
curl --location --request GET 'https://besttime.app/api/v1/forecasts/week/raw?api_key_public=pub_e11661721b084d36b8f469a2c012e754&venue_id=ven_51387131543761435650505241346a394a6432395362654a496843'
```

```javascript
var settings = {
    "url": "https://besttime.app/api/v1/forecasts/week/raw",
    "data": {
        'api_key_public': 'pub_e11661721b084d36b8f469a2c012e754',
        'venue_id': 'ven_51387131543761435650505241346a394a6432395362654a496843'
    },
    "method": "GET"
};

$.ajax(settings).done(function (response) {
    console.log(response);
});
```

### Input attributes

The 'query week raw' endpoint is used to retrieve the raw data from an existing forecast (every day of the week).

- **venue_id** `string` <span style="color:orange">REQUIRED</span>  
 The unique ID for the venue. The venue_id can be retrieved from a 'new forecast' endpoint response, or by the 'all venues' endpoint which shows all previously forecasted venues.  
 &nbsp; 
- **api_key_public** `string` <span style="color:orange">REQUIRED</span>  
 Public API Key. See more info on [API keys](#api-keys)  
 &nbsp; 

<aside class="notice">
New forecast endpoint: https://BestTime.app/api/v1/forecasts/week/raw
</aside>

<aside class="notice">
HTTP method: GET
</aside>

<aside class="warning">
The week raw endpoint is only available for platinum subscribers.
</aside>

> The above request returns JSON structured like this:

```json
{
    "analysis": {
        "week_raw": [
            0.0,
            10.0,
            30.0,
            60.0,
            80.0,
            90.0,
            100.0,
            Other hours hidden 
            50.0,
            40.0,
            40.0,
            30.0,
            10.0,
            0.0,
            0.0
        ]
    },
    "epoch_analysis": 1585875838,
    "forecast_updated_on": "2020-04-03T01:03:58.692417+00:00",
    "venue_name": "McDonald's"
}
```
