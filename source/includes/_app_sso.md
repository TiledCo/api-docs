# App SSO

## HTTP based authentication

> Example SSO universal link

```
https://app.tiled.co/app/sso/?
  url=https%3A%2F%2Fmy.auth.provider&
  apiToken=1234abcd5678efgh&
  usernameLabel=email&
  usernameKey=user.email&
  passwordKey=user.password&
  emailPath=user.profile.login&
  namePath=user.profile.firstName&
  namePath=user.profile.lastName&
  storeCredentials=true
```

> For this example, and the username of `bob@example.com` and password of `fancypants`, the following will POST to `https://my.auth.provider`:
>

```json
{
  "user": {
    "email": "bob@example.com",
    "password": "fancypants"
  }
}
```

> The default POST body if `usernameKey` and `passwordKey` were not set would look like:

```json
{
  "username": "bob@example.com",
  "password": "fancypants"
}
```

> And we are expecting a JSON result of the form:

```json
{
  "user": {
    "profile": {
      "login": "bob@example.com",
      "firstName": "Bob",
      "lastName": "Johnson"
    }
  }
}
```

> You can see `emailPath` and the two `namePath` parameters will allow the app to correctly parse the result and extract `bob@example.com` as the email address to use for finding the correct tiled user in our system.
> The name parsed from this results would be `Bob Johnson`.

Use this method to authenticate with third party identity providers.

### Universal Link

`https://app.tiled.co/app/sso/`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
url | true | none | The url for your identity provider's authorization endpoint.
apiToken | true | none | Your Tiled API token - generated in **account settings** on <a href="https://app.tiled.co" target="_blank">https://app.tiled.co</a>.
emailPath | true | none | The **path** to the user's email address in the response body.
namePath | true | none | The **path** to the user's name in the response body. If the user name is in multiple parts, they can be specified with multiple instances of `namePath` parameters and the results will be joined with a space at runtime.
expirationPath | false | null | The **path** to an optional session expiration date in the response body.
method | false | POST | HTTP method to use when accessing `url`.
usernameLabel | false | username | The placeholder text for the username form input in the app.
passwordLabel | false | password | The placeholder text for the password form input in the app.
usernameKey | false | username | The **path** in the request body to set the username in the request sent to `url`.
passwordKey | false | password | The **path** in the request body to set the password in the request sent to `url`.
ttl | false | null | How long the session should last (in milliseconds or a <a href="https://www.npmjs.com/package/ms" target="_blank">string representation</a> e.g. "24h", "30m", "12345s", "4d"). Note, if `expirationPath` is set and a valid date is found using it, `ttl` will not be used.
formTitle | false | Sign in | The title displayed at the top of the sign in form in the app.
formLogo | false | null | A URL to an image to display at the top of the sign in form in the app. The logo is letterboxed in a rectangle 306x80. Note - if set, `formTitle` will not be used.
primaryColor | false | #eb2227 | The background color of the sign in button and the text color of the form inputs. Note, the sign in button text color is white.
storeCredentials | false | false | If this is true, the user's credentials are stored in the device Keychain and when a session expires the user can authenticate with TouchID or 4-digit PIN to get a new session.

<aside class="warning">
Remember — make sure all your url parameters are encoded!
</aside>



## Web based authentication

> Example SSO universal link

```
https://app.tiled.co/app/sso/?
  idp=fancypantsapp&
  ttl=24h
```

Use this method to authenticate with third party identity providers using a web-based OAuth, OpenID, SAML or other flow.

<aside class="notice">
This form of SSO requires custom configuration by Tiled engineers. Contact us if you are interested in this form of SSO.
</aside>

### Universal Link

`https://app.tiled.co/app/sso/`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
id | true | none | A unique ID provided by Tiled
ttl | false | null | How long the session should last (in milliseconds or a <a href="https://www.npmjs.com/package/ms" target="_blank">string representation</a> e.g. "24h", "30m", "12345s", "4d"). Note - if `ttl` is not set, the session will not expire unless manually revoked on the Tiled website.

<aside class="warning">
Remember — make sure all your url parameters are encoded!
</aside>



## Using custom auth tokens

> Example SSO universal link

```
https://app.tiled.co/app/auth/?
  idp=fancypantsapp&
  token=1234abcd5678efgh
  ttl=24h
```

Use this method if you want to generate and sign a secure token and send it directly into the app to authenticate the user.

<aside class="notice">
This form of SSO requires custom configuration by Tiled engineers. Contact us if you are interested in this form of SSO.
</aside>

### Universal Link

`https://app.tiled.co/app/sso/`

### Query Parameters

Parameter | Required | Default | Description
--------- | -------- | ------- | -----------
id | true | none | A unique ID provided by Tiled
token | true | none | A signed token containing the user's email address for lookup
ttl | false | null | How long the session should last (in milliseconds or a <a href="https://www.npmjs.com/package/ms" target="_blank">string representation</a> e.g. "24h", "30m", "12345s", "4d"). Note - if `ttl` is not set, the session will not expire unless manually revoked on the Tiled website.

<aside class="warning">
Remember — make sure all your url parameters are encoded!
</aside>
