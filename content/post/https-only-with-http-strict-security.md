---
date: 2015-03-11
title: "HTTPS only with HTTP Strict Transport Security (HTST) header"
tags: [ "http", "web", "code", "nginx" ]
categories: [ "development" ]
---

The HTTP Strict Transport Security header (`Strict-Transport-Security`) allows you to tell the brower to only communicate with a site using HTTPS. Once the browser has successfully connected using HTTPS and seen the header, it will only communicate with the site using HTTPS from that point forward, changing the protocol if needed. By enabling this header you can prevent man-in-the-middle attacks via [SSL stripping](https://en.wikipedia.org/wiki/SSL_stripping#SSL_stripping).

There is a good overview @ [Mozilla](https://developer.mozilla.org/en-US/docs/Security/HTTP_Strict_Transport_Security) on the header and its benefits.

### Browser support
Most browsers support it with the exception of IE which is coming soon.

- Chrome (4)
- Internet Explorer (IE12)
- Firefox (4)
- Opera (12)
- Safari (Mac OS X 10.9)

### Nginx example

```nginx
server {
  listen 443 ssl default deferred;
  server_name site.com;

  ssl_certificate /etc/nginx/ssl/site_com.crt;
  ssl_certificate_key /etc/nginx/ssl/site_com.key;

  # Enable HSTS(HTTP Strict Transport Security)
  add_header Strict-Transport-Security "max-age=31536000; includeSubdomains;";
}
```
