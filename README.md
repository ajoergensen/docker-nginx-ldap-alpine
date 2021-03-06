#  **[nginx][3]** built with **OpenSSL 1.1.1** (TLSv1.3 support) and LDAP support

WIP - Still need templating of LDAP configuration

## Features

- Uses [Alpine Linux][5] as base
- PCRE with JIT enabled
- HTTP/2.0 (+NPN) support
- Async I/O using threads support
- [Cloudflare Dynamic TLS records][6] patch
- [Brotli][7] compression support
- [ngx_headers_more][12] module from [OpenResty][13]
- [Cloudlare's HPACK][14] patch for full [HPACK][15] header compression support.
- [nginx-auth-ldap][ldap] - LDAP Authentication module for nginx

## Usage

```docker run --rm --name nginx -v ./htdocs:/var/www -p 80:80 -p 443:443 -d ajoergensen/nginx-libressl:tag```

Available tags are `stable` and `mainline`

## Environment

- `PUID`: Change the uid of the user running nginx
- `PGID`: Change the gid of the user running nginx
- `CHOWN_WWWDIR`: Enable/disable the change of ownership of /var/www to $PUID:$PGID, defaults to TRUE. Note, if /var/www read only this variable will always be FALSE
- `WORKER_PROCESSES`: Change the value of nginx worker_processes, defaults to auto.
- `NGINX_CLIENT_MAX_BODY_SIZE`: Set `client_max_body_size`, default is 50M.
- `SERVER_TOKENS`: Controls `server_tokens`. Set to `on` or `off`. Default is `off`
- `CUSTOM_SERVER`: Sets the `Server:` header to a custom value. Default is undefined.

## Other

Though not defined as a volume, I recommend mapping a folder to /etc/nginx/conf.d to store your vhost definitions.

This image works great with [docker-gen][8] and [docker-letsencrypt-nginx-proxy-companion][9] (as a drop-in replacement for the nginx-proxy image)

----

Originally based on the official nginx Dockerfile & `Wonderfall/boring-nginx` - Forked from [denji/nginx-libressl][1]

[1]: https://github.com/nginx-modules/docker-nginx-libressl/
[3]: http://nginx.org/
[4]: https://libressl.org/
[5]: https://alpinelinux.org/
[6]: https://blog.cloudflare.com/optimizing-tls-over-tcp-to-reduce-latency/
[7]: https://en.wikipedia.org/wiki/Brotli
[8]: https://github.com/jwilder/nginx-proxy
[9]: https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion
[11]: https://blog.cloudflare.com/deprecating-spdy/
[12]: https://github.com/openresty/headers-more-nginx-module
[13]: https://openresty.org/en/
[14]: https://github.com/cloudflare/sslconfig
[15]: https://http2.github.io/http2-spec/compression.html
[nginx_patch]: https://github.com/kn007/patch/blob/master/nginx.patch
[ldap]: https://github.com/kvspb/nginx-auth-ldap
