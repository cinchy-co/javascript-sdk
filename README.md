# Cinchy Javascript-SDK

## Installation

Add the cinchy.js file to your project and include the script in the html pages that use it.

Example:
```html
<script src="js/cinchy.js"></script>
```

Please use v2.x.x of the library if you are using Cinchy v2.x.x and higher,
otherwise, use v1.x.x.

## Configure

To connect to Cinchy, you must configure the window's cinchyJS object in your javascript code:

```javascript
window.cinchyJS = new CinchyJS({
    // The url of your Cinchy instance
    cinchyRootUrl: 'http://my.cinchy.url.co',
    // The identity server of your Cinchy instance
    authority: 'http://my.cinchy.url.co/cinchyssocore',
    // The client id for your applet
    client_id: 'javascript-sample',
    // (Optional) The requested scopes for the applet (must be permitted for the client)
    // You must have openid and id requested
    scope: 'openid id email profile roles',
    // (Optional) Enable silent refresh
    silent_refresh_enabled: true,
    // (Optional) (Mandatory if silentRefreshEnabled = true) The silent refresh url
    silent_redirect_uri: 'http://localhost:3000/silent-refresh.html',
    // The callback function that gets executed after login
    user_loaded_callback: initialize
});
```

## Enabling Silent Refresh

In order to use silent refresh, you must:

1). Set the silent_refresh_enabled property to true in your CinchyJS object.

2). Add a silent-refresh.html file into your project. This can be found within the repo folder in the repo or copy & paste this (modify the script src location to where your cinchy.js file is):

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
</head>
<body>
    <script src="/js/cinchy.js"></script>
    <script>
        new Oidc.UserManager().signinSilentCallback().catch((err) => {
            console.log(err);
        });
    </script>
</body>
</html>
```
Silent refresh works by using a hidden iframe to access a url that contains the silent-refresh.html page. This iframe makes a request to the server to retrieve a new access token.

3). Add the silent-refresh url into the "Permitted Login Redirect URLs" field of the "Integrated Clients" table within Cinchy (eg. http://localhost:3000/silent-refresh.html).

## License
This project is license under the terms of the [GNU General Public License v3.0](https://github.com/cinchy-co/javascript-sdk/blob/master/LICENSE)