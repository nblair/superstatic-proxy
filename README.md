# Superstatic Proxy Service [![Travis](https://img.shields.io/travis/divshot/superstatic-proxy.svg?style=flat-square)](https://travis-ci.org/divshot/superstatic-proxy)

The Superstatic AJAX proxy lets you make requests to other domians without
violating the Same-Origin Policy. For instance, you could mount a proxy
called `api` that pointed to `https://api.your-app.com`. Once you've done
so, a request to e.g. `/api/users.json` would be proxied through to
`https://api.your-app.com/api/users.json`.

## Configuration

The configuration for `superstatic-proxy` is an object where the keys are
reference names for the service to which you're proxying and configuration
details. An example (comments for clarity despite JSON syntax):

```js
{
  "api": {
    // the origin of the server to which you want to make requests
    "origin": "https://api.your-app.com",
    
    // set default headers present on every request. these can be
    // overridden on individual AJAX requests
    "headers": {
      "Accept": "application/json"
    },
    
    // if true, send the cookies from the static app along to the server
    "cookies": false,
    
    // set a timeout for requests sent to the proxy (defaults to 30 seconds)
    "timeout": 30,
    
    // rewrite URLs before proxying (default list is empty)
    // the first path fragment of source must match the name of this config ('api' in this example)
    "rewrites": [
      { "source": "/api/proxy", "destination": "/" }
    ]
  }  
}
```