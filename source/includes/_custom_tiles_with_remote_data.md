# Custom Tiles with Remote Data

## Overview

Custom tiles can be configured to fetch remote data for rendering. This documentation outlines the configuration values you can use and how they work.


## Configuring remote URL

> Example URL **without** query string parameters

```
// ENTERED URL
https://www.example.com/user/data
```

```
// REQUEST URL
https://www.example.com/user/data?
  userId=am9obmRvZUBleGFtcGxlLmNvbQ%3D%3D
```

You provide a URL where the data needed for the custom tile can be accessed. The URL will be access with an `HTTP GET` request with the current user's ID appended as the query string parameter `userId`.

The user ID is their `email address` that has been `base64` encoded.

<aside class="notice">
You can add other query string parameters in the URL body as you wish. If you provide your own parameters, `userId` will be appended to the end of the url.
</aside>


## Response

> Example response

```json
{
  "label": "My custom label",
  "body": "Some great body copy",
  "color": "#0080ff"
}
```

The URL you provide should return a valid `JSON object` with the `Content-Type` header set to `application/json`

The data you return will be used to override the default values (configurable in the hub editor) for the custom tile.

