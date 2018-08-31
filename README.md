# Hello Storage

A local storage resolution which help developer to use localStorage/sessionStorage storage mode easliy.

## Install

```
npm install --save hello-storage
```

## Usage
ES6: 

```
import HelloStorage from 'hello-storage/src/hello-storage'
```

With pack tools like webpack:

```
import HelloStorage from 'hello-storage'
```

CommonJS:

```
const HelloStorage = require('hello-storage')
```

AMD & CMD:

```
define(function(require, exports, module) {
  const HelloStorage = require('hello-storage')
})
```

Normal Browsers:

```
<script src="./node_modules/hello-storage/dist/hello-storage.js"></script>
```

```
window.HelloStorage
```

To use:

```
import HelloStorage from 'hello-storage'

let store = new HelloStorage({
  storage: sessionStorage, // required
  namespace: 'my.ns', // required
  expires: 10*60,
})

store.set('my_key', { value: 'ok' })

let value = store.get('my_key') // { value: 'ok' }
```

## Options

**namespace**

String to prepend to each key. It is recommended to use '.' like 'com.docker.service.data'.

Notice: two HelloStorage instances SHOULD NOT have same namespace, or same conflict may come out.

**expires**

How long the value will be expired. Unit is second(1s). If you set '0', it means the value will never expire.

**storage**

Which storage driver do you want to use: localStorage, sessionStorage, AsyncStorage. 
[AsyncStorage](https://facebook.github.io/react-native/docs/asyncstorage.html) is used for react-native, when you pass AsyncStorage, options.async should MUST be `true`.

**async**

If options.async is set to be true, all methods will return a promise, so that you can use async functions easliy:

```
let store = new HelloStorage({
  ...
  async: true,
})

(async function() {
  let value = await store.get('my_key')
})()
```

## Methods

### set(key, value, expires)

Add a data to the storage. `key` is a string, which will be connected with 'namespace'. `value` can be object.

```
store.set('the_key', 'value')
```

If expires is not set, options.expires will be used.

### get(key)

Get data from storage by key. If no data found by the key, or the data is expired, `null` will be returned.

### remove(key)

Remove a certain data from the storage by key.

### clean()

Clean the whole store data.

### getAllKeys()

Return all keys of this namespace.
