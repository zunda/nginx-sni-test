# nginx-sni-test
A test app to check nginx configuration as a proxy to an SNI endpoint

I could confirm that [adding lines like `proxy_ssl_server_name on;` and `proxy_ssl_name <host name for SNI extension>;`](config/nginx.conf.erb#L47-L48) makes nginx work as expected:

## Procedure
### Deploy to Heroku
Clone this repository and

```
heroku create
heroku buildpacks:set https://github.com/dubsmash/nginx-buildpack
git push heroku master
```

### Access to the proxy
Note the `HTTP_X_FORWARDED_PROTO` and `HTTP_X_FORWARDED_PORT` headers

Target: http://ssl.zunda.ninja/env
(the endpoint is on Heroku SSL as of writing this)

Proxy through
- HTTP: http://*app_name*.herokuapp.com/env
- HTTPS with SNI enabled: http://*app_name*.herokuapp.com/sni/env
- HTTPS with SNI disabled: http://*app_name*.herokuapp.com/noni/env -
  shows 502 Bad Gateway
