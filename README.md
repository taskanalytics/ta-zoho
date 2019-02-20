# Zoho OAuth2 Utilities

Zoho's v2 API integration relies on an OAuth2 authentication flow, requiring users to generate refresh tokens for use in their applications. In practice it's not hard, but getting the initial refresh token is often a headache.

Google's Cloud SDK does this well: when you authenticate with Google to grant your client access to your Google Cloud APIs it handles popping your browser and prompting you to authenticate and grant API access. They nicely redirect you to a special page that displays the grant token that you then give to the client to request the initial refresh token.

Zoho doesn't have a standard redirect page like that, so it's up to the developer/end-user to stage one. This is simply done via spinning up a temporary local http server to simplify extracting the grant token.

## OAuth 2.0 Authenticator Client
To execute: `npm run auth` or `node cli.js`

Currently expects some environment variables until these are transitioned to command line args:

| Variable             | Description                            | Required? | Default Value                                                      |
|----------------------|----------------------------------------|:---------:|--------------------------------------------------------------------|
| `ZOHO_CLIENT_ID`     | Zoho App Client Id                     |    Yes    |                                                                    |
| `ZOHO_CLIENT_SECRET` | Zoho App Client Secret                 |    Yes    |                                                                    |
| `ZOHO_REDIRECT_URI`  | Zoho App Redirect URI                  |     No    | `http://localhost:8888/zoho/callback`                              |
| `ZOHO_REDIRECT_HOST` | Hostname or IP for binding http server |     No    | `localhost` (so chances are this binds to 127.0.0.1)               |
| `ZOHO_REDIRECT_PORT` | TCP Port to bind for http server       |     No    | `8888`                                                             |
| `ZOHO_SCOPE`         | Zoho API access scope to request       |     No    | `ZohoCRM.modules.Leads.CREATE` (you might want to change this)     |

If cli args end up implemented, expect `ZOHO_CLIENT_SECRET` to be passed via `stdin`.

## Zoho API Wrapper
TODO: implement some helper functions for calling Zoho and handling generating new access tokens when they expire.

# Assorted Notes About Zoho's Defaults
* It seems Zoho's access tokens default to a 3600s (1 hr) expiration. This doesn't look configurable.
* Zoho claims you can "see" your active tokens in your Zoho account profile screen, yet as of 18 Dec 2018 that doesn't seem to be the case.
* See Zoho's [OAuth docs](https://www.zoho.com/crm/help/api/v2/#oauth-request) for more details.

# License
We're providing this under an [ISC License](./LICENSE)
