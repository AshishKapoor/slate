
# BigQuery

This page will help you get started with Rill Data. You'll be up and running in a jiffy!

```javascript
// Example code snippit
const rilldata = require('rilldata');

let api = rilldata.authorize('rill-service-key');
let rilldata = api.rilldata.get();
```

```ruby
require 'rilldata'

example code snippet
```

```python
import rilldata

api = rilldata.authorize('rill-service-key')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: rill-service-key"
```

```javascript
const rill = require('rilldata');

let api = rill.authorize('rill-service-key');
```

> Make sure to replace `rill-service-key` with your API key.

Maybe have a link to Rill API support [developer portal](http://example.com/developers).

`Authorization: rill-service-key`

<aside class="notice">
You must replace <code>rill-service-key</code> with your personal API key.
</aside>


### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the rill item to delete

