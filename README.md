This is a slightly modified version of Django's built-in FetchFromCacheMiddleware that allows for simple bypassing of the cache for requests that don't rely on views (and thus you can't use the @never_cache decorator). Just install, and create a list of regex urls that you don't want cached.

Installation

1) Place the file somewhere you app can find it.

2) Then add Django's "UpdateCacheMiddleware" and "CustomFetchFromCacheMiddleware" to your settings.py

MIDDLEWARE_CLASSES = (
    'django.middleware.cache.UpdateCacheMiddleware',
    '...',
    '...',
    'path.to.customcachemiddleware.CustomFetchFromCacheMiddleware'
)

3) Add a list of urls you want the cache to bypass.

CACHE_BYPASS_URLS = (
    r'/no/cache/url/',   
)

4) Profit!

I use it in conjunction with uwsgi's in-memory cache and django-tastypie:

http://projects.unbit.it/uwsgi/wiki/CachingFramework
https://github.com/toastdriven/django-tastypie

I wrote about my use case for this on my blog:

http://www.jnhasty.com/2012/11/08/caching-api-requests-with-django-tastypie-nginx-and-uwsgi/

And big ups to this article for helping me come to this solution: 
http://soyrex.com/articles/django-nginx-memcached/

