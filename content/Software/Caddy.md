---
public: true
---


## AuthP
[authp](https://authp.github.io/) is a Caddy Authentication Portal plugin.

## Logging in Caddy

Use [log directive](https://caddyserver.com/docs/caddyfile/directives/log#output-modules) in Caddyfile within a site.

```
beta.jamesravey.me {
   root * /path/to/brainsteam/_site
   file_server
   log {
       output file /var/log/caddy/brainsteam-access.log {
           roll_size 2M
           roll_keep 10
       }
   }
   #reverse_proxy localhost:12380
}

```