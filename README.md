# nginx-sni-test
A test app to check nginx configuration as a proxy to an SNI endpoint

I could confirm that [adding lines like `proxy_ssl_server_name on;` and `proxy_ssl_name <host name for SNI extension>;`](https://github.com/zunda/nginx-sni-test/blob/master/config/nginx.conf.erb#L47-L48) makes nginx work as expected.
