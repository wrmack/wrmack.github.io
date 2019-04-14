---
layout: page
title: Bind
subtitle: Setting up Bind
use-site-title: true
show-avatar: false
---
## Install

```
brew install bind
```

## Configure
Execute following in a terminal.

### Create configuration files:

```
/usr/local/sbin/rndc-confgen | tee -a /usr/local/etc/rndc.conf
head -n 6 /usr/local/etc/rndc.conf | tee -a /usr/local/etc/rndc.key`
```

### Create named.conf.  

Start an editor:

```
sudo nano
```

Copy and paste the following into it:

```
	//
	// Include keys file
	//
	include "/usr/local/etc/rndc.key";
	// Declares control channels to be used by the rndc utility.
	//
	// It is recommended that 127.0.0.1 be the only address used.
	// This also allows non-privileged users on the local host to manage
	// your name server.
	//
	// Default controls
	//
		
	controls {
	        inet 127.0.0.1 port 54 allow {any;}
	        keys { "rndc-key"; };
	};
	options {
	        directory "/usr/local/var/named";
	};
	// 
	// a caching only nameserver config
	// 
	zone "." IN {
	    type hint;
	    file "named.ca";
	};
	zone "localhost" IN {
	    type master;
	    file "localhost.zone";
	    allow-update { none; };
	};
	zone "test" IN {
	type master;
	file "test.zone";
	};
	zone "0.0.127.in-addr.arpa" IN {
	    type master;
	    file "named.local";
	    allow-update { none; };
	};
	logging {
	        category default {
	                _default_log;
	        };
	        channel _default_log  {
	                file "/usr/local/var/log/named/named.log";
	                severity info;
	                print-time yes;
	        };
	};
```
Save to: 
```
/usr/local/etc/named.conf
```

Note that the configuration above creates a "test" zone.  This will make it possible to create a host name of macbook.test.  Replace 'test' with your preferred domain name.

## Create test.zone
If you created a custom zone with a different name then use that name:  
```
[yourname].zone
```

Using an editor like nano paste the following.  This maps macbook.test to the ip address of the computer.  Change these to suit your own setup.


```
	$TTL    86400
	$ORIGIN test.
	@       7200    IN      SOA @ root.test. (
	                                20190222        ; serial
	                                3H              ; refresh every 15 mins
	                                15M             ; retry every 3 hours
	                                1W              ; expiry
	                                1D)             ; minimum
	;
	                IN      NS      localhost.
	macbook.test.   IN      A       192.168.1.13
	*.macbook.test. IN      A       192.168.1.13

```


Save to 
```
/usr/local/var/named/test.zone
```

Create a directory that bind will use for saving files: `mkdir /usr/local/var/named`

```
curl http://www.internic.net/domain/named.root | tee -a /usr/local/var/named/named.ca
```

## /etc/hosts
Not sure if this is necessary but I mapped 127.0.0.1 to the domain:

```
	##
	# Host Database
	#
	# localhost is used to configure the loopback interface
	# when the system is booting.  Do not change this entry.
	##
	127.0.0.1       localhost
	255.255.255.255 broadcasthost
	::1             localhost
	127.0.0.1       macbook.test
	127.0.0.1       *macbook.test
```

## Start
Either:
```
sudo /usr/local/opt/bind/sbin/named
```

or start as a service:
```
sudo brew services start bind
```

## Documentation
Documentation is not installed with the brew installation. Have to download the tarball from the bind website and go to docs:
```
/[path to bind]/bind-9.12.3-P4/doc/arm/Bv9ARM.ch03.html
```

## Utilities
These are helpful for testing setup:

```
dscacheutil -flushcache
dig
scuttle —dns
ping
/usr/local/sbin/named-xxx
```
Check named is running with 
```
sudo ps -ef|grep named
``` 
or check with Activity Monitor.
