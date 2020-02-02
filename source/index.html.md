---
title: sCORe API
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - javascript--nodejs: Node.JS
  - ruby: Ruby
  - python: Python
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

<h1 id="score-api">sCORe API v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

# Introduction  
  
Welcome to the sCORe API. The api consists of multiple high-performance RESTful JSON endpoints that can be used to fetch the data about performance and reputation of different chainlink oracles.  
test test
  
We have client libraries in [python](https://github.com/securedatalinks/reputation-score-python-client),[golang](https://github.com/securedatalinks/reputation-score-golang-client) and [nodejs](https://github.com/securedatalinks/reputation-score-js-client) generated from [swagger file](#TODO)! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.  
  
  
# Quick Start Guide  
```shell  
# With shell, you can just pass the correct header with each request  
curl "api_endpoint_here"  
  -H "Authorization: API_KEY"  
  curl -X POST -d "from=9870454" -d "to=9877754" -d "oracle_url=0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D" reputation.link/reputation-interval
```
  
For developers eager to start using sCORe API right away, there are 3 quick steps to make.  
  
1. Sign up for a free API access key on [reputation.link](reputation.link)  
2. (optional) If you own an oracle, register your oracle on the same page to be able to get more info about your oracle.  
3. Make a test call using your API key. Check example on the right that fetches the most up-to-date reputation for all oracles;  
  

# Authentication  
  
## Obtaining API key  
sCORe uses API keys to allow access to the API. All requests made against the sCORe api must be validated with API key. In order to get API key, you must register at [reputation.link](http://reputation.link).  
  
## Using API key  
  
> Example using auth in request body   
  
```ruby  
  
#TODO  
  
```
  
```python  
#TODO  
```
  
```shell  
# With shell, you can just pass the correct header with each request  
curl "api_endpoint_here"  
  -H "Authorization: API_KEY"  
  curl -X POST -d "from=9870454" -d "to=9877754" -d "oracle_url=0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D" reputation.link/reputation-interval
```
  
```javascript  
#TODO  
  
```
> Make sure to replace `API_KEY` with your API key.  
  
API key must be included in all API requests to the server.  
There are 2 ways to supply API key with your call:  
  
1. In an HTTP header that looks like : `Authorization: API_KEY`  
2. Via additional parameter in request body : `Authorization: "API_KEY"`  
  
<aside class="notice">  
You must replace <code>API_KEY</code> with your personal API key.  
</aside>  
  
# Standards and conventions  
  
## Endpoint Response Payload Format  
Each endpoint returns data in JSON format with 2 parts, `data` and `status`.  
A `data` object contains results for request if the call is successful.  
A `status` object contains the timestamp, when the call was executed and status code and message, indicating if the request was succesfull  
See [status codes and rate limits](#status-codes-and-rate-limits) for details in different status codes.   
  
```
{  
  "data" : {  
    ...  
  },  
  "status": {  
    "timestamp": "2018-06-06T07:52:27.273Z",  
    "status_code": 400,  
    "error_message": "Invalid value for \"id\"",  
  }  
}  
```
## Versioning  
The sCORe API is versioned to guarantee new features and updates are non-breaking. The latest version of this API is /V1/.  
All our API endpoints start with version.  
  
Backwards compatible updates might be added to API without creating new version. You can check our [Changelog](#Changelog) to see those changes.  
These updates are considered backwards compatible:  
  
 * Adding new API resources.  
 * Adding new optional request parameters to existing API methods.  
 * Adding new properties to existing API responses.  
 * Changing the order of properties in existing API responses.  
 * Changing the way some data are computed, while not changing the range of possible values     
      -- e.q. We change the way reputation of oracle is computed, but it's still a value between 1 and 100.  
  
  
##TODO maybe we should add minor versions, like stripe, maybe it's overkill  
https://stripe.com/docs/api/versioning  
  
## Date and Time Formats  
All endpoints that require date/time parameters allow timestamps to be passed in either `yyyy-mm-dd hh:mm:ss` (eq.2018-06-22 01:46:40) timestamp format or in Unix time (eg. 1528249600).  
All timestamps returned in JSON payloads are returned in UTC time using human-readable format which follows this pattern: `yyyy-mm-dd hh:mm:ss`  
Data is collected, recorded, and reported in UTC time unless otherwise specified.  
  
## Status codes and rate limits  
Every endpoint always respond with HTTP status code 200 for both succesful requests and failures. The `status` object is always included in the JSON response. This object contains `status_code` and `error_message`.  
If there was a problem processing the request, one of these status codes is returned.  
  
Error Code |  Error Message  
-----------|---------------  
1000 | Request was succesful  
1001 | This API Key is invalid.  
1002 | API key missing.  
1003 | Invalid request parameters  
1004 | Your don't have permissions for this call.  
1005 | This API Key has been disabled. Please contact support.  
1006 | You've exceeded your API Key's HTTP request rate limit.   
1007 | You've exceeded your API Key's daily rate limit.  
1008 | You've exceeded your API Key's monthly rate limit.  
  
The rate limits are:    
XXXX per day    
xxxx per month #TODO  

## Cache / Update frequency
All data are updated every 5 minutes.

# Endpoint overview  
  
Endpoint |  Error Message  
-----------|---------------  
[/V1/reputations/historical](#historical-reputation) | historical reputations of one or more oracles
[/V1/reputation/latest](#latest-reputation) | latest reputation of one or more oracles  
[/V1/key/info](#API-key-metadata) | metadata about used API key (rate limits, permissions...)  
[/V1/oracles/info](#oracle-info) | Public info about one or more oracles
[/V1/reputations/full/latest](#oracle-latest-full-data) | All monitored data about given oracle. Only for oracle owners.
[/V1/reputations/full/historical](#oracle-historical-full-data) | All historical monitored data about given oracle. Only for oracle owners.

Base URLs:

* <a href="https://reputation.link:3001/">https://reputation.link:3001/</a>

Email: <a href="mailto:ashley@securedatalinks.com">Support</a> 
License: <a href="http://www.apache.org/licenses/LICENSE-2.0.html">Apache 2.0</a>

<h1 id="score-api-public">Public</h1>

Operations for retrieval of public data about oracles

## historical reputations of one or all oracles

<a id="opIdrephist"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://reputation.link:3001/V1/reputations/historical?from=0&to=0&oracle_address=string \
  -H 'Accept: application/json' \
  -H 'Authentication: string'

```

```http
GET https://reputation.link:3001/V1/reputations/historical?from=0&to=0&oracle_address=string HTTP/1.1
Host: reputation.link:3001
Accept: application/json
Authentication: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authentication':'string'

};

$.ajax({
  url: 'https://reputation.link:3001/V1/reputations/historical',
  method: 'get',
  data: '?from=0&to=0&oracle_address=string',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authentication':'string'

};

fetch('https://reputation.link:3001/V1/reputations/historical?from=0&to=0&oracle_address=string',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authentication' => 'string'
}

result = RestClient.get 'https://reputation.link:3001/V1/reputations/historical',
  params: {
  'from' => 'integer',
'to' => 'integer',
'oracle_address' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authentication': 'string'
}

r = requests.get('https://reputation.link:3001/V1/reputations/historical', params={
  'from': '0',  'to': '0',  'oracle_address': 'string'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://reputation.link:3001/V1/reputations/historical?from=0&to=0&oracle_address=string");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authentication": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://reputation.link:3001/V1/reputations/historical", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /V1/reputations/historical`

Returns each update of reputation between from and to timestamps for given oracle

<h3 id="historical-reputations-of-one-or-all-oracles-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|from|query|integer|true|Get only reputation after|
|to|query|integer|true|Get only reputations before|
|oracle_address|query|string|true|Get only reputations for giver oracle. If missing, get all oracles that were active between from and to|
|Authentication|header|string|true|none|

> Example responses

> 200 Response

```json
[
  {
    "timestamp": 97521541,
    "network": "Ropsten",
    "oracle_address": 1.0094115432877367e+48,
    "reputation": 95.4,
    "total_requests": 1400,
    "total_responses": 1399,
    "link_earned": 1450,
    "avg_response_time": 0.99,
    "uptime": 0.999,
    "unique_requestors": 40,
    "gas_price": 134057,
    "assignment_complete_ratio": 0.99
  }
]
```

<h3 id="historical-reputations-of-one-or-all-oracles-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A User object|[ReputationArray](#schemareputationarray)|

<aside class="success">
This operation does not require authentication
</aside>

## get last reputation for one or all oracles

<a id="opIdreplate"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://reputation.link:3001/V1/reputations/latest?oracle_address=string \
  -H 'Accept: application/json' \
  -H 'Authentication: string'

```

```http
GET https://reputation.link:3001/V1/reputations/latest?oracle_address=string HTTP/1.1
Host: reputation.link:3001
Accept: application/json
Authentication: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authentication':'string'

};

$.ajax({
  url: 'https://reputation.link:3001/V1/reputations/latest',
  method: 'get',
  data: '?oracle_address=string',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authentication':'string'

};

fetch('https://reputation.link:3001/V1/reputations/latest?oracle_address=string',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authentication' => 'string'
}

result = RestClient.get 'https://reputation.link:3001/V1/reputations/latest',
  params: {
  'oracle_address' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authentication': 'string'
}

r = requests.get('https://reputation.link:3001/V1/reputations/latest', params={
  'oracle_address': 'string'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://reputation.link:3001/V1/reputations/latest?oracle_address=string");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authentication": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://reputation.link:3001/V1/reputations/latest", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /V1/reputations/latest`

Returns latest update of reputation of given oracle

<h3 id="get-last-reputation-for-one-or-all-oracles-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|oracle_address|query|string|true|Get only reputations for given oracle. If missing, get all oracles that were active between from and to|
|Authentication|header|string|true|none|

> Example responses

> 200 Response

```json
{
  "timestamp": 97521541,
  "network": "Ropsten",
  "oracle_address": 1.0094115432877367e+48,
  "reputation": 95.4,
  "total_requests": 1400,
  "total_responses": 1399,
  "link_earned": 1450,
  "avg_response_time": 0.99,
  "uptime": 0.999,
  "unique_requestors": 40,
  "gas_price": 134057,
  "assignment_complete_ratio": 0.99
}
```

<h3 id="get-last-reputation-for-one-or-all-oracles-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|See status error codes for error reporting|[Reputation](#schemareputation)|

<aside class="success">
This operation does not require authentication
</aside>

## Meta information about key, rate limits, user

<a id="opIdgetKeyInfo"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://reputation.link:3001/V1/key/info \
  -H 'Accept: application/json' \
  -H 'Authentication: string'

```

```http
GET https://reputation.link:3001/V1/key/info HTTP/1.1
Host: reputation.link:3001
Accept: application/json
Authentication: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authentication':'string'

};

$.ajax({
  url: 'https://reputation.link:3001/V1/key/info',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authentication':'string'

};

fetch('https://reputation.link:3001/V1/key/info',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authentication' => 'string'
}

result = RestClient.get 'https://reputation.link:3001/V1/key/info',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authentication': 'string'
}

r = requests.get('https://reputation.link:3001/V1/key/info', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://reputation.link:3001/V1/key/info");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authentication": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://reputation.link:3001/V1/key/info", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /V1/key/info`

Returns info about given API KEY

<h3 id="meta-information-about-key,-rate-limits,-user-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authentication|header|string|true|none|

> Example responses

> 200 Response

```json
{
  "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
  "name": "Widget Adapter",
  "nasdf": "Widget Adapter",
  "releaseDate": "2016-08-29 09:12:33 UTC"
}
```

<h3 id="meta-information-about-key,-rate-limits,-user-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|See status error codes for error reporting|[Key_info](#schemakey_info)|

<aside class="success">
This operation does not require authentication
</aside>

## metadata about oracles

<a id="opIdOracles"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://reputation.link:3001/V1/oracles/info?oracle_addres=string \
  -H 'Accept: application/json'

```

```http
GET https://reputation.link:3001/V1/oracles/info?oracle_addres=string HTTP/1.1
Host: reputation.link:3001
Accept: application/json

```

```javascript
var headers = {
  'Accept':'application/json'

};

$.ajax({
  url: 'https://reputation.link:3001/V1/oracles/info',
  method: 'get',
  data: '?oracle_addres=string',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://reputation.link:3001/V1/oracles/info?oracle_addres=string',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://reputation.link:3001/V1/oracles/info',
  params: {
  'oracle_addres' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://reputation.link:3001/V1/oracles/info', params={
  'oracle_addres': 'string'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://reputation.link:3001/V1/oracles/info?oracle_addres=string");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://reputation.link:3001/V1/oracles/info", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /V1/oracles/info`

Returns public information about oracle

<h3 id="metadata-about-oracles-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|oracle_addres|query|string|true|Get only reputations for given oracle. If missing, get all oracles that were active between from and to|

> Example responses

> 200 Response

```json
{
  "name": "ACME Corporation",
  "homePage": "https://www.acme-corp.com",
  "phone": "408-867-5309"
}
```

<h3 id="metadata-about-oracles-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|See status error codes for error reporting|[Oracle_info](#schemaoracle_info)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="score-api-oracle-owners">Oracle owners</h1>

Operations available to oracle owners

## All historical data used for computing reputation

<a id="opIdfulhist"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://reputation.link:3001/V1/reputations/owner/historical?oracle_addres=string \
  -H 'Accept: application/json'

```

```http
GET https://reputation.link:3001/V1/reputations/owner/historical?oracle_addres=string HTTP/1.1
Host: reputation.link:3001
Accept: application/json

```

```javascript
var headers = {
  'Accept':'application/json'

};

$.ajax({
  url: 'https://reputation.link:3001/V1/reputations/owner/historical',
  method: 'get',
  data: '?oracle_addres=string',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://reputation.link:3001/V1/reputations/owner/historical?oracle_addres=string',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://reputation.link:3001/V1/reputations/owner/historical',
  params: {
  'oracle_addres' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://reputation.link:3001/V1/reputations/owner/historical', params={
  'oracle_addres': 'string'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://reputation.link:3001/V1/reputations/owner/historical?oracle_addres=string");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://reputation.link:3001/V1/reputations/owner/historical", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /V1/reputations/owner/historical`

Returns all oracle performance data from given timeframe. The oracle must be registered on reputation.link with the account associated with API key.

<h3 id="all-historical-data-used-for-computing-reputation-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|oracle_addres|query|string|true|Addres of oracle|

> Example responses

> 200 Response

```json
[
  {
    "timestamp": 97521541,
    "network": "Ropsten",
    "oracle_address": 1.0094115432877367e+48,
    "reputation": 95.4,
    "total_requests": 1400,
    "total_responses": 1399,
    "link_earned": 1450,
    "avg_response_time": 0.99,
    "uptime": 0.999,
    "unique_requestors": 40,
    "gas_price": 134057,
    "assignment_complete_ratio": 0.99
  }
]
```

<h3 id="all-historical-data-used-for-computing-reputation-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|See status error codes for error reporting|[ReputationArray](#schemareputationarray)|

<aside class="success">
This operation does not require authentication
</aside>

## metadata about oracle

<a id="opIdfullatest"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://reputation.link:3001/V1/reputations/owner/latest/?oracle_addres=string \
  -H 'Accept: application/json'

```

```http
GET https://reputation.link:3001/V1/reputations/owner/latest/?oracle_addres=string HTTP/1.1
Host: reputation.link:3001
Accept: application/json

```

```javascript
var headers = {
  'Accept':'application/json'

};

$.ajax({
  url: 'https://reputation.link:3001/V1/reputations/owner/latest/',
  method: 'get',
  data: '?oracle_addres=string',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://reputation.link:3001/V1/reputations/owner/latest/?oracle_addres=string',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://reputation.link:3001/V1/reputations/owner/latest/',
  params: {
  'oracle_addres' => 'string'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://reputation.link:3001/V1/reputations/owner/latest/', params={
  'oracle_addres': 'string'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://reputation.link:3001/V1/reputations/owner/latest/?oracle_addres=string");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://reputation.link:3001/V1/reputations/owner/latest/", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /V1/reputations/owner/latest/`

Returns public information about oracle

<h3 id="metadata-about-oracle-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|oracle_addres|query|string|true|Returns latest oracle performance data. The oracle must be registered on reputation.link with the account associated with API key.|

> Example responses

> 200 Response

```json
{
  "timestamp": 97521541,
  "network": "Ropsten",
  "oracle_address": 1.0094115432877367e+48,
  "reputation": 95.4,
  "total_requests": 1400,
  "total_responses": 1399,
  "link_earned": 1450,
  "avg_response_time": 0.99,
  "uptime": 0.999,
  "unique_requestors": 40,
  "gas_price": 134057,
  "assignment_complete_ratio": 0.99
}
```

<h3 id="metadata-about-oracle-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|See status error codes for error reporting|[Reputation](#schemareputation)|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocSreputation">Reputation</h2>

<a id="schemareputation"></a>

```json
{
  "timestamp": 97521541,
  "network": "Ropsten",
  "oracle_address": 1.0094115432877367e+48,
  "reputation": 95.4,
  "total_requests": 1400,
  "total_responses": 1399,
  "link_earned": 1450,
  "avg_response_time": 0.99,
  "uptime": 0.999,
  "unique_requestors": 40,
  "gas_price": 134057,
  "assignment_complete_ratio": 0.99
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|timestamp|integer(timestamp)|true|none|none|
|network|string|true|none|none|
|oracle_address|string|true|none|none|
|reputation|number|true|none|none|
|total_requests|integer|true|none|none|
|total_responses|integer|true|none|none|
|link_earned|integer|true|none|none|
|avg_response_time|number|true|none|none|
|uptime|number|true|none|none|
|unique_requestors|integer|true|none|none|
|gas_price|integer|true|none|none|
|assignment_complete_ratio|number|true|none|none|

<h2 id="tocSreputationarray">ReputationArray</h2>

<a id="schemareputationarray"></a>

```json
[
  {
    "timestamp": 97521541,
    "network": "Ropsten",
    "oracle_address": 1.0094115432877367e+48,
    "reputation": 95.4,
    "total_requests": 1400,
    "total_responses": 1399,
    "link_earned": 1450,
    "avg_response_time": 0.99,
    "uptime": 0.999,
    "unique_requestors": 40,
    "gas_price": 134057,
    "assignment_complete_ratio": 0.99
  }
]

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Reputation](#schemareputation)]|false|none|none|

<h2 id="tocSkey_info">Key_info</h2>

<a id="schemakey_info"></a>

```json
{
  "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
  "name": "Widget Adapter",
  "nasdf": "Widget Adapter",
  "releaseDate": "2016-08-29 09:12:33 UTC"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string(uuid)|false|none|none|
|name|string|false|none|none|
|nasdf|string|false|none|none|
|releaseDate|string(date-time)|false|none|none|

<h2 id="tocSoracle_info">Oracle_info</h2>

<a id="schemaoracle_info"></a>

```json
{
  "name": "ACME Corporation",
  "homePage": "https://www.acme-corp.com",
  "phone": "408-867-5309"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|none|
|homePage|string(url)|false|none|none|
|phone|string|false|none|none|

