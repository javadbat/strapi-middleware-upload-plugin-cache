# strapi-middleware-upload-plugin-cache

## Use case
- 'strapi-provider-upload-local' is in use for uploading assets via ``Media Library`` in Strapi
- the need for configurable cache-control HTTP response headers (e.g. ``cache-control: max-age=1234``) + [ETag HTTP response header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag) for each asset
- more information and differences between ``koa-static`` (used in 'strapi-provider-upload-local') and ``koa-static-cache`` (used in this middleware-plugin) can be found [here](https://github.com/koajs/static-cache)

## Installing
Using npm

```
npm install --save strapi-middleware-upload-plugin-cache
```

Using yarn

```
yarn add strapi-middleware-upload-plugin-cache
```

## Setup
For Strapi, add a ``middleware.js`` file within the config folder

e.g.
```
touch config/middleware.js
```

containing

```
module.exports = ({ env }) => ({
  settings: {
    'upload-plugin-cache': {
      enabled: true,
      maxAge: 86400000
    }
  }
});

```

Starting Strapi in dev-mode should log the following:
```
[2020-12-30T21:37:57.560Z] debug [UploadCache] Initializing middleware ...
[2020-12-30T21:37:57.561Z] debug [UploadCache] Middleware initialized for endpoint='/uploads/(.*)' [maxAge=86400000]
```


## Configuration Options
With the option ``dynamic: true`` files which are not cached on initializations are dynamically loaded. To avoid OOM errors a [LRU-cache can be used](https://www.npmjs.com/package/@zhennann/koa-static-cache#using-a-lru-cache-to-avoid-oom-when-dynamic-mode-enabled). For config options of lru-cache use these [docs](https://www.npmjs.com/package/lru-cache) and insert them at ``lruCache``.

```
module.exports = ({ env }) => ({
  settings: {
    'upload-plugin-cache': {
      enabled: true,
      maxAge: 86400000,
      dynamic: true,
      lruCache: {
        max: 1000
      }
    }
  }
});

```


## Resources

- [License](LICENSE)

## Links

- [Strapi website](http://strapi.io/)
- [Strapi community on Slack](http://slack.strapi.io)
- [Strapi news on Twitter](https://twitter.com/strapijs)