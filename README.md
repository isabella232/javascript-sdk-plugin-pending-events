# @optimizely/sdk-plugin-pending-events

An [`EventDispatcher`](https://developers.optimizely.com/x/solutions/sdks/reference/index.html?language=javascript#event-dispatcher) for Optimizely FullStack ([`javascript-sdk`](https://github.com/optimizely/javascript-sdk), Web browser environment)
that keeps a queue of pending (not completed) events and persist to localStorage. This allows us to retry events that are canceled by e.g. a page unload.

## Install

```sh
npm install @optimizely/sdk-plugin-pending-events
```

## Usage

See [`example`](./example) for an example of how this is used:

```sh
$ cd example
$ npm install
$ npm start
```

Load index.html in browser of your choice.

### API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### SendJSONCallback

[src/index.js:105-131](https://github.com/optimizely/javascript-sdk-plugin-pending-events/blob/b59e84950ca9460e0ec08556c66eb82de0599fb7/src/index.js#L61-L64 "Source code on GitHub")

Type: [Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)

**Parameters**

-   `error` **[Error](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Error)?** Error, if any

#### SendJSON

[src/index.js:105-131](https://github.com/optimizely/javascript-sdk-plugin-pending-events/blob/b59e84950ca9460e0ec08556c66eb82de0599fb7/src/index.js#L66-L95 "Source code on GitHub")

Function to call to send JSON

Type: [Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)

**Parameters**

-   `url` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** URL to send to
-   `options` **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** 
    -   `options.method` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** HTTP method to use
    -   `options.body` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Body text (should be stringified JSON)
-   `callback` **[SendJSONCallback](#sendjsoncallback)** Function to call, with no arguments, if successful, and with Error object, if error

**Examples**

```javascript
// Example sendJSON built using fetch
const sendJSON = (url, options, callback) => {
  const {method, body} = options;
  return fetch(url, {
    method,
    body,
    headers: {
      'content-type': 'application/json',
    }
  })
  .then((resp) => {
    if (resp.status < 400) {
      callback();
    } else {
      callback(new Error(`Bad response code: ${resp.status}`));
    }
  }, callback);
}
```

#### index

[src/index.js:105-131](https://github.com/optimizely/javascript-sdk-plugin-pending-events/blob/b59e84950ca9460e0ec08556c66eb82de0599fb7/src/index.js#L105-L131 "Source code on GitHub")

Construct an EventDispatcher compatible with @optimizely/optimizely-sdk

**Parameters**

-   `localStorageKey` **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** Key under which to persist/load pending events in `window.localStorage`
-   `sendJSON` **[SendJSON](#sendjson)** Function to call to send payload
-   `logger` **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)?** 

Returns **EventDispatcher** An object with a dispatchEvent method, suitable for use as an EventDispatcher
