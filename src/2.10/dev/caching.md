---
title: Caching
type: guide
version: "2.10"
order: 16
---

Cement defines a cache interface called [ICache](/{{ version }}/api/core/cache.html#cement.core.cache.ICache), but does not implement caching by default.  The documentation below references usage based on the interface and not the full capabilities of any given implementation.

The following cache handlers are included and maintained with Cement:

- [MemcachedCacheHandler](/{{ version }}/api/ext/ext_memcached.html#cement.ext.ext_memcached.MemcachedCacheHandler)
- [RedisCacheHandler](/{{ version }}/api/ext/ext_redis.html#cement.ext.ext_redis.RedisCacheHandler)


Please reference the [ICache](/{{ version }}/api/core/cache.html#cement.core.cache.ICache) interface documentation for writing your own cache handler.

## General Usage

For this example we use the Memcached extension, which requires the `pylibmc` library to be installed, as well as a Memcached server running on localhost.

Example:

**/path/to/myapp.conf**

```
[myapp]
extensions = memcached

[cache.memcached]
# comma separated list of hosts to use
hosts = 127.0.0.1

# time in milliseconds
expire_time = 300
```

**myapp.py**

```python
from cement.core.foundation import CementApp

with CementApp('myapp') as app:
    # run the application
    app.run()

    # set a cached value
    app.cache.set('my_key', 'my value')

    # get a cached value
    app.cache.get('my_key')

    # delete a cached value
    app.cache.delete('my_key')

    # delete the entire cache
    app.cache.purge()
```
