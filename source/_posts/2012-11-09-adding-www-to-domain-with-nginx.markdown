---
layout: post
title: "Adding www to domain with nginx"
date: 2012-11-09 08:49
comments: true
categories: tips
tags:
 - nginx
 - tips
---
###Adding www to domain with nginx

With [nginx](http://wiki.nginx.org/) it's quite easy to add www to your domain name when access your website.
```
# Add a www to the domain
server {
  listen 80;
  server_name example.com;
  rewrite ^(.*)$ $scheme://www.example.com$1;
}
```
With this, any request to `example.com` will be changed to `www.example.com`. 