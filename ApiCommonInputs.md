Parameters that all (nearly) API methods support.

| Parameter | Description | Default value | Example |
|:----------|:------------|:--------------|:--------|
| `client`  | Identifier for the program making the API requests. Especially meant for browser-based applications that do not control the user agent. | _none_        | `feedly` |
| `T`       | ActionToken (required for `POST` requests) | _none_        | `//RQ5Ala9wTbGxisuYqJALKg` |
| `hl`      | Language to use for the response. If not specified, will be inferred based on`Accept-Language` HTTP header, IP, user preferences, etc. | _none_        | `en`    |

Parameters that most API methods that return data support.

| Parameter | Description | Default value | Example |
|:----------|:------------|:--------------|:--------|
| `output`  | Output format. Possible values are `json` ([JavaScript Object Notation](http://www.json.org/)) and `xml` (an XML representation of JSON). | `xml`         | `json`  |

See also [Authentication](Authentication.md) for authentication-related parameters that should be provided to all methods that require authentication.