---
layout: page
title: Development environment
subtitle: My debugging setup
use-site-title: true
show-avatar: false
--- 

## Intro
In order to debug a native iOS app interacting with a node solid server running locally, it is necessary to:
- provide node solid server with ssl keys (because it runs over https)
- run a DNS server if you want to run your app on a device and interact with the server (you cannot simply use ip addresses, solid server assigns sub-domains to users)

## Hardware & software setup
- Computer: Macbook Pro
- IDE for developing iOS apps: Xcode
- Editor for debugging solid-server: Visual Studio Code 

## Prepare ssl keys
When you initialize solid server you need to provide the paths to your ssl keys.

In order to interact over the network using https, keys are needed for solid server and a certificate is needed for each device you run your app on.

Follow the instructions here:
[Apple instructions](https://developer.apple.com/library/archive/technotes/tn2326/_index.html#//apple_ref/doc/uid/DTS40014136)

You create a root certificate and then a digital identity certificate from which you export your private and public keys.  

## Set up a DNS server
Solid-server by default runs on localhost. Say you have an app on a device which is separate to the computer solid server is running on (but the device is on the same network) and you want to access solid server from your app. You cannot give it localhost as the url. You might be able to use your ip address but if you start adding users you need a domain with subdomains.

There are a number of DNS servers available.  I installed [BIND](https://www.isc.org/downloads/bind/). Installation [run-through](../Bind).
 
## Install node solid server
I installed locally rather than globally so I had easy access to source files.  In a terminal:

* create a directory for installing solid server
* cd to the directory then install solid-server
* Do:
```
npm install solid-server
```

Initialise solid-server: 

- The server uri will use the domain name you set up when setting up the DNS server
- You probably want to answer Y to multi-user mode
- Do:
```
/[path to node modules]/node_modules/solid-server/bin/solid init
```

