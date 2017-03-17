# Forever sessions
Normally JWT session tokens can only be refreshed prior to the DF_JWT_REFRESH_TTL timer expiring. By enabling forever sessions you can force the system to ignore DF_JWT_REFRESH_TTL and allow refresh at any time (forever). The session token will still expire after DF_JWT_TTL and require refreshing, but it can be refreshed forever.

### Configuration
#### 1. Set DF_ALLOW_FOREVER_SESSIONS
In <code>...\apps\dreamfactory\htdocs\.env</code>, add or un-comment this line and set the value to true:
```js
DF_ALLOW_FOREVER_SESSIONS=true
```

To make sure forever session is enabled, make the following API call.
```js
GET http://{url}/api/v2/system/environment
```
Look for the following in your response.

```js
"allow_forever_sessions":true
```

#### 2. Set DF_JWT_TTL
In <code>...\apps\dreamfactory\htdocs\.env</code>, add or un-comment this line and set the value to your desired TTL in minutes. A session refresh will be required to receive a new session token after this many minutes.
```js
DF_JWT_TTL=1440
```
The above setting will require a session refresh every 24 hours (1440 minutes).

#### 3. Clear config
Run this command from the root directory for your DreamFactory instance installation.
```js
  ...\apps\dreamfactory\htdocs>php artisan config:clear
  ...\apps\dreamfactory\htdocs>php artisan cache:clear
```
