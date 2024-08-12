Timeout settings:

If time is provided in the derectives below, then it is default nginx values.

### ngx_http_core_module
https://nginx.org/en/docs/http/ngx_http_core_module.html

- client_body_timeout
- client_header_timeout
- keepalive_timeout
- lingering_timeout
- resolver_timeout 30s _(timeout for DNS resolution)_
- send_timeout 60s _(timeout for the client to receive something)_

### ngx_http_proxy_module
https://nginx.org/en/docs/http/ngx_http_proxy_module.html

- proxy_cache_lock_timeout
- proxy_next_upstream_timeout
- proxy_connect_timeout 60s _(timeout for establishing a connection with the proxied server)_ __502 Bad Gateway__
- proxy_send_timeout 60s _(timeout for the proxied server to receive something)_
- proxy_read_timeout 60s _(timeout for the proxied server to respond something)_ __504 Gateway Time-out__

### ngx_http_ssl_module
https://nginx.org/en/docs/http/ngx_http_ssl_module.html

- ssl_session_timeout
