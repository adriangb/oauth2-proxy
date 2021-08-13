# To test run:

```bash
$ make nginx-up
```

And now navigate to [http://httpbin.oauth2-proxy.localhost/get](http://httpbin.oauth2-proxy.localhost/get).
If you're using Chrome, this should just work.
If you're using another browser (or `curl`), add these entries to `/etc/hosts`:

```text
127.0.0.1 oauth2-proxy.localhost
127.0.0.1 httpbin.oauth2-proxy.localhost
127.0.0.1 oauth2-proxy.oauth2-proxy.localhost
```

You should be redirected to log in. The credentials are:

- `username`: admin@example.com
- `password`: password

Once you log in, you'll be redirected back to the `httpbin` response, which will include an `Authorization` header that holds the JWT access token that the IdP generated.
You can copy this token and make requests from `curl` or do other programmatic access things:

```bash
$ export MY_TOKEN="<token you copied above>"
$ curl -H "Accept: application/json" -H "Authorization: Bearer $MY_TOKEN" -L http://httpbin.oauth2-proxy.localhost/get
```

You'll get the same JSON response as before, but without the login process.

If you put an invalid token in the header, you'll get a 401.
