---
sidebar_position: 20
sidebar_label: Example
title: Momento Proxy Example Config
description: View an example configuration file for Momento Proxy
---

# Example configuration file

Below is an example configuration file for running Momento Proxy. When no config file is explicitly set when the docker image is launched, the one below is used automatically.

```toml
[admin]
# interfaces listening on
host = "0.0.0.0"
# port listening on
port = "9999"

[proxy]
# restrict the number of threads to use, defaults to number of CPUs
# threads = 1

# One or more caches must be specified. Each listens on its own port and directs
# requests to a specific Momento cache.

[[cache]]
# interfaces listening on
host = "0.0.0.0"
# port listening on
port = "11211"
# the name of the Momento cache to direct requests to
cache_name = "users"
# the TTL, in seconds, to use when items are set as 'no expiry' (TTL is zero)
# NOTE: accepted values are between 1 and 4_294_967 (inclusive)
default_ttl = 900
# the protocol can be "memcache" or "resp" (Redis), the default is memcache
# protocol = "memcache"

[[cache]]
# interfaces listening on
host = "0.0.0.0"
# port listening on
port = "11212"
# the name of the Momento cache to direct requests to
cache_name = "products"
# the TTL, in seconds, to use when items are set as 'no expiry' (TTL is zero)
# NOTE: accepted values are between 1 and 4_294_967 (inclusive)
default_ttl = 1800
# the protocol can be "memcache" or "resp" (Redis), the default is memcache
protocol = "memcache"

[[cache]]
# interfaces listening on
host = "0.0.0.0"
# port listening on
port = "6379"
# the name of the Momento cache to direct requests to
cache_name = "ratings"
# the TTL, in seconds, to use when items are set as 'no expiry' (TTL is zero)
# NOTE: accepted values are between 1 and 4_294_967 (inclusive)
default_ttl = 300
# the protocol can be "memcache" or "resp" (Redis), the default is memcache
protocol = "resp"

# Configure the proxy's logging

[debug]
# choose from: error, warn, info, debug, trace
log_level = "info"
# optionally, log to the file below instead of standard out
# log_file = "momento-proxy.log"
# backup file name for use with log rotation
log_backup = "momento-proxy.log.old"
# trigger log rotation when the file grows beyond this size (in bytes). Set this
# option to '0' to disable log rotation.
log_max_size = 1073741824

# Configure the logging of commands

[klog]
# optionally, log commands to the file below
# file = "momento-proxy.cmd"
# backup file name for use with log rotation
backup = "momento-proxy.cmd.old"
# trigger log rotation when the file grows beyond this size (in bytes). Set this
# option to '0' to disable log rotation.
max_size = 1073741824
# specify the sampling ratio, 1 in N commands will be logged. Setting to '0'
# will disable command logging.
sample = 100
```
