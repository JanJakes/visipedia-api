# 2. Oauth2

OAuth2 is a protocol that lets external applications request user's private data without getting their password.

## 2.1 Application registration
First of all the developers must register their application on ___. The reqistration process will assign the application a unique `client_id` and `client_secret`.

## 2.2 OAuth2 flow for web applications

1. **Redirecting the user to Visipedia authentication server**

   ```
   GET https://visipedia.org/oauth2/authorize
   ```

   Parameters:

   | Name           | Type   | Description |
   | -------------- | ------ | ----------- |
   | **client_id**  | string | The Client ID for your application obtained during the registration. |
   | redirect_uri   | string | The URI where the user will be redirected after authorization. If not provided the URI from your app settings will be used. If provided, the domain part must match the URI in the settings. |
   | scope          | string | A list of scopes ___. |
   | state          | string | CSRF? |

   The user will se a screen asking him to authorize Visipedia to give your app the requested scopes.
2. **Redirecting back to your site**

   When the user accepts your request, Visipedia redirects back to your site. A `code` and `state` parameters will be passed with the request.
3. **Requesting the Access Token**

   ```
   POST https://visipedia.org/oauth2/access_token
   ```

   Parameters:

   | Name              | Type   | Description |
   | ----------------- | ------ | ----------- |
   | **client_id**     | string | The Client ID for your application obtained during the registration. |
   | **client_secret** | string | The Client Secret for your application obtained during the registration. |
   | **code**          | string | The code received in the previous step. |
   | redirect_uri      | string | ... |

4. **Receiving the Access Token**
   
5. **Using the Access Token**
