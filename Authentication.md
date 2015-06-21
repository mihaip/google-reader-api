# OAuth (preferred) #

[OAuth](http://code.google.com/apis/accounts/docs/GettingStarted.html#OAuth) is the preferred authentication mechanism for both [web](http://code.google.com/apis/accounts/docs/OAuth.html) and [installed](http://code.google.com/apis/accounts/docs/OAuthForInstalledApps.html) apps. Using the scope `https://www.google.com/reader/api/` obtain a request token, authorize it, exchange it for an access token, and make requests as usual, passing in the OAuth token in the `Authorization:` HTTP header. You may find the [OAuth Playground](http://googlecodesamples.com/oauth_playground/index.php) useful in experimenting with all this.

The `https://www.google.com/reader/atom/` and `https://www.google.com/reader/subscription/export` scopes are supported as well for applications wish to use the Atom and OPML outputs. Additionally, HTTP versions of these HTTPS schemes  are also available.

# ClientLogin #

Installed (desktop) apps may also use [ClientLogin](http://code.google.com/apis/accounts/docs/AuthForInstalledApps.html) to perform authenticated requests against Google Reader's API. The app provides the user's username and password, and obtains an authentication token in response (the value after `Auth=` in the response). That token can be be included as an HTTP header in all requests (format `Authorization:GoogleLogin auth=<auth value>`).

`service` should be set to `reader`. `accountType` should be set to `GOOGLE` (Google Reader does not support hosted accounts).

Sample `curl` request to get the authentication token:

```
$ curl -d accountType=GOOGLE \
  -d Email=username@gmail.com \
  -d Passwd=password \
  -d service=reader \
  https://www.google.com/accounts/ClientLogin
SID=<SID value> # ignored
LSID=<LSID value> # ignored
Auth=<auth value>
```

Sample `curl` request that uses the authentication token:

```
$ curl -H "Authorization:GoogleLogin auth=<auth value>" http://www.google.com/reader/api/0/user-info
{
  "userId":"123",
  "userName":"Name",
  "userProfileId":"123",
  "userEmail":"username@gmail.com",
  "isBloggerUser":true,
  "signupTimeSec":0,
  "publicUserName":"username"
}
```

Clients should also handle CAPTCHA challenges, see the [documentation](http://code.google.com/apis/accounts/docs/AuthForInstalledApps.html#AuthProcess) for more information.