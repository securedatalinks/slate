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

The sCORe API consists of multiple high-performance RESTful JSON endpoints that can be used to fetch data relevant to the historical performance and reputation of Chainlink Oracles. 
  
There are client libraries written in [python](https://github.com/securedatalinks/reputation-score-python-client), [golang](https://github.com/securedatalinks/reputation-score-golang-client) and [nodejs](https://github.com/securedatalinks/reputation-score-js-client) generated from [swagger file](#TODO). If you require different language functionality then be sure to get into contact.
  
  
# Quick Start Guide  

* Sign up for a free API key on [reputation.link](reputation.link). 
* If you operate an Oracle then be sure to register to to display your performance data on our frontend as well as gain full access to the sCORe API depending on your subscription. 
* Once your key has been generated, make a test call to ensure functionality. 
* Check the example on the right, which fetches the up-to-date data relating to the Secure Data Links Oracle.
  
### "@Tomas we need a name here":

Provide description of this: 

```shell  
  curl -X POST -d "from=9870454" -d "to=9877754" -d "oracle_url=0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D" -H "Authorization: API_KEY" reputation.link/reputation-interval
```

@Tomas 'BE CLEARER HERE - Here is an example using auth in HTTP headers'. Make sure to replace `API_KEY` with your newly generated key.  

```shell   
curl -X POST -H "Authorization: API_KEY"  -d "from=1580083200" -d "to=1580183200" -d "oracle_url=0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D" reputation.link/reputation-interval
```
  
The API key must be included in all API requests via the HTTP header:

`Authorization: API_KEY`  
  

    
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

* Each endpoint returns data in JSON format with 2 parts, `data` and `status`.  
* A `data` object contains results for the request if the call is successful.  
* A `status` object contains the timestamp, when the call was executed, the status code and message which will  indicate if the request was succesfull.  
* See [status codes and rate limits](#status-codes-and-rate-limits) for details on different status codes.

The sCORe API is versioned to ensure that any updates do not break anything. The latest version of this API is V1.0.0.  When testing the sCORe API ensure that the version you are using is correct.  
  
Backwards compatible updates may be added to the API without creating new version. You can check our [Changelog](#Changelog) (@Tomas ??) to see those changes.  

  
 * Adding new API resources.  
 * Adding new optional request parameters to existing API methods.  
 * Adding new properties to existing API responses.  
 * Changing the order of properties in existing API responses.  
 * Changing the way some data are computed, while not changing the range of possible values
  
* All endpoints that require date/time parameters allow timestamps to be passed in as either `yyyy-mm-dd hh:mm:ss` (eq.2018-06-22 01:46:40) format or in Unix time frp,at (eg. 1528249600).  
* All timestamps returned in JSON payloads are returned in UTC time using a human-readable format which follows this pattern: `yyyy-mm-dd hh:mm:ss`  
* Data is collected, recorded, and reported in UTC time unless otherwise specified.  
  
* Every endpoint responds with HTTP status code 200 for both succesful requests and failures. The `status` object is always included in the JSON response. This object contains `status_code` and `error_message`.  
* If there was a problem processing the request, one of these status codes is returned.
  
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
  
Each key can be used to query the endpoint up to 30 times per minute.

At this point all data are updated every 5 minutes. 

  
Endpoint |  Error Message  
-----------|---------------  
[/V1/reputations/historical](#historical-reputation) | Historical data relating to an individual or multiple oracles
[/V1/reputation/latest](#latest-reputation) | Latest data relating to an individual or multiple oracles  
[/V1/key/info](#API-key-metadata) | Metadata relating to the API key used  
[/V1/oracles/info](#oracle-info) | Public information relating to an individual or multiple oracless
[/V1/reputations/full/latest](#oracle-latest-full-data) | Latest snapshot relating to the owners oracle
[/V1/reputations/full/historical](#oracle-historical-full-data) | All historical monitored data about given oracle. Only for oracle owners.

Base URLs:

* <a href="https://reputation.link:3001/">https://reputation.link:3001/</a>

Email: <a href="mailto:inquiry@reputation.link">Support</a> 
License: <a href="http://www.apache.org/licenses/LICENSE-2.0.html">Apache 2.0</a>

<h1 id="score-api-public">Public</h1>

Operations for retrieval of public reputation data.

## historical reputations of one or all oracles

<a id="opIdrephist"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://reputation.link:3001/V1/reputations/historical?start=0&end=0&oracle_address=string \
  -H 'Accept: application/json' \
  -H 'Authentication: string'

```

```http
GET https://reputation.link:3001/V1/reputations/historical?start=0&end=0&oracle_address=string HTTP/1.1
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
  data: '?start=0&end=0&oracle_address=string',
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

fetch('https://reputation.link:3001/V1/reputations/historical?start=0&end=0&oracle_address=string',
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
  'start' => 'integer',
'end' => 'integer',
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
  'start': '0',  'end': '0',  'oracle_address': 'string'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://reputation.link:3001/V1/reputations/historical?start=0&end=0&oracle_address=string");
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

Returns each update of reputation between start and end periods for a given oracle

<h3 id="historical-reputations-of-one-or-all-oracles-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|start|query|integer|true|Get data after|
|end|query|integer|true|Get data before|
|oracle_address|query|string|true|Get performance data for a specified oracle. If missing, get all oracles that were active between start and end periods|
|Authentication|header|string|true|none|

> Example responses

> 200 Response

```json
[
  {
    "timestamp": 97521541,
    "network": "Ropsten",
    "oracle_address": "0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D",
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
|oracle_address|query|string|true|Get performance data for a specified oracle. If missing, get all oracles that were active between start and end periods|
|Authentication|header|string|true|none|

> Example responses

> 200 Response

```json
{
  "timestamp": 97521541,
  "network": "Ropsten",
  "oracle_address": "0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D",
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

## Meta information relating to a specific API key

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

<h3 id="meta-information-relating-to-a-specific-api-key-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|Authentication|header|string|true|none|

> Example responses

> 200 Response

```json
{
  "email": "oraclereputation@chainlink.com",
  "owned_oracles": "0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D",
  "remaining_rate_limit": 23
}
```

<h3 id="meta-information-relating-to-a-specific-api-key-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|See status error codes for error reporting|[Key_info](#schemakey_info)|

<aside class="success">
This operation does not require authentication
</aside>

## Metadata on oracles

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

Returns public data relevant to an oracle

<h3 id="metadata-on-oracles-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|oracle_addres|query|string|true|Get performance data for a specified oracle. If missing, get all oracles that were active between start and end periods|

> Example responses

> 200 Response

```json
{
  "name": "SDL Oracle",
  "website": "Secure Data Links",
  "url_name": "www.securedatalinks.com",
  "contact_email": "admin@securedatalinks.com",
  "email": "admin@securedatalinks.com",
  "description": "Integrate with the Secure Data Links Oracle",
  "oracle_address": "0x2Ed7E9fCd3c0568dC6167F0b8aEe06A02CD9ebd8",
  "location": "Brisbane, Australia",
  "node_hosting": "Hosted locally with GCP backups",
  "eth_node_hosting": "GCP"
}
```

<h3 id="metadata-on-oracles-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|See status error codes for error reporting|[Oracle_info](#schemaoracle_info)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="score-api-oracle-owners">Oracle owners</h1>

Operations available to oracle owners who registered their oracle on reputation.link

## All historical data relating to an oracle

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

Returns all oracle performance data within a specified timeframe. The oracle must be registered on reputation.link with an account associated with their respective API key.

<h3 id="all-historical-data-relating-to-an-oracle-parameters">Parameters</h3>

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
    "oracle_address": "0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D",
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

<h3 id="all-historical-data-relating-to-an-oracle-responses">Responses</h3>

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

Returns public Oracle information

<h3 id="metadata-about-oracle-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|oracle_addres|query|string|true|Returns latest oracle performance data. The oracle must be registered on reputation.link with an account associated with their respective API key.|

> Example responses

> 200 Response

```json
{
  "timestamp": 97521541,
  "network": "Ropsten",
  "oracle_address": "0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D",
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
  "oracle_address": "0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D",
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
    "oracle_address": "0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D",
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
  "email": "oraclereputation@chainlink.com",
  "owned_oracles": "0xB0Cf943Cf94E7B6A2657D15af41c5E06c2BFEA3D",
  "remaining_rate_limit": 23
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|email|string|true|none|none|
|owned_oracles|string|true|none|none|
|remaining_rate_limit|integer|true|none|none|

<h2 id="tocSoracle_info">Oracle_info</h2>

<a id="schemaoracle_info"></a>

```json
{
  "name": "SDL Oracle",
  "website": "Secure Data Links",
  "url_name": "www.securedatalinks.com",
  "contact_email": "admin@securedatalinks.com",
  "email": "admin@securedatalinks.com",
  "description": "Integrate with the Secure Data Links Oracle",
  "oracle_address": "0x2Ed7E9fCd3c0568dC6167F0b8aEe06A02CD9ebd8",
  "location": "Brisbane, Australia",
  "node_hosting": "Hosted locally with GCP backups",
  "eth_node_hosting": "GCP"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|true|none|none|
|website|string|true|none|none|
|url_name|string|true|none|none|
|contact_email|string|true|none|none|
|email|string|true|none|none|
|description|string|true|none|none|
|oracle_address|string|true|none|none|
|location|string|true|none|none|
|node_hosting|string|true|none|none|
|eth_node_hosting|string|true|none|none|

