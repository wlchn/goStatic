# goStatic [![Docker Pulls](https://img.shields.io/docker/pulls/wlchn/gostatic.svg?style=plastic)](https://hub.docker.com/r/wlchn/gostatic/) [![Docker Build](https://img.shields.io/docker/build/wlchn/gostatic.svg?style=plastic)](https://hub.docker.com/r/wlchn/gostatic/)
Forked from PierreZ/goStatic, changed the base image from `scratch` to `alpine`, so that we can use sh in it, but still keep small.


A really small static web server for Docker

### The goal
My goal is to create to smallest docker container for my web static files. The advantage of Go is that you can generate a fully static binary, so that you don't need anything else.

### Wait, I've been using old versions of GoStatic and things have changed!

Yeah, decided to drop support of unsecured HTTPS. Two-years ago, when I started GoStatic, there was no automatic HTTPS available. Nowadays, thanks to Let's Encrypt, it's really easy to do so. If you need HTTPS, I recommend [caddy](https://caddyserver.com).

### Features
 * A fully static web server in 6MB
 * No frameworkw
 * Web server build for Docker
 * Can generate certificate on his own
 * Light container
 * More security than official images (see below)
 * Log enabled

### Why?
Because the official Golang image is wayyyy to big (around 1/2Gb as you can see below) and could be unsecure.

[![](https://badge.imagelayers.io/golang:latest.svg)](https://imagelayers.io/?images=golang:latest 'Get your own badge on imagelayers.io')

For me, the whole point of containers is to have a light container...
Many links should provide you with additionnal info to see my point of view:

 * [Over 30% of Official Images in Docker Hub Contain High Priority Security Vulnerabilities](http://www.banyanops.com/blog/analyzing-docker-hub/)
 * [Create The Smallest Possible Docker Container](http://blog.xebia.com/2014/07/04/create-the-smallest-possible-docker-container/)
 * [Building Docker Images for Static Go Binaries](https://medium.com/@kelseyhightower/optimizing-docker-images-for-static-binaries-b5696e26eb07)
 * [Small Docker Images For Go Apps](https://www.ctl.io/developers/blog/post/small-docker-images-for-go-apps)

### How to use
```
docker run -d -p 80:8043 -v path/to/website:/srv/http --name goStatic pierrezemb/gostatic
```

### Usage 

```
./goStatic --help
Usage of /goStatic:
  -append-header HeaderName:Value
        HTTP response header, specified as HeaderName:Value that should be added to all responses.
  -context string
        The 'context' path on which files are served, e.g. 'doc' will serve the files at 'http://localhost:<port>/doc/'
  -default-user-basic-auth string
        Define the user (default "gopher")
  -enable-basic-auth
        Enable basic auth. By default, password are randomly generated. Use --set-basic-auth to set it.
  -fallback string
    	Default relative to be used when no file requested found. E.g. /index.html
  -password-length int
        Size of the randomized password (default 16)
  -path string
        The path for the static files (default "/srv/http")
  -port int
        The listening port (default 8043)
  -set-basic-auth string
        Define the basic auth. Form must be user:password
```
