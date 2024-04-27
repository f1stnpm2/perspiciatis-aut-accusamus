# @f1stnpm2/perspiciatis-aut-accusamus

![GitHub Workflow Status (branch)](https://img.shields.io/github/actions/workflow/status/RyanZim/@f1stnpm2/perspiciatis-aut-accusamus/ci.yml?branch=master)
![Coveralls github branch](https://img.shields.io/coveralls/github/RyanZim/@f1stnpm2/perspiciatis-aut-accusamus/master.svg)
![npm](https://img.shields.io/npm/dm/@f1stnpm2/perspiciatis-aut-accusamus.svg)
![npm](https://img.shields.io/npm/l/@f1stnpm2/perspiciatis-aut-accusamus.svg)

Make a callback- or promise-based function support both promises and callbacks.

Uses the native promise implementation.

## Installation

```bash
npm install @f1stnpm2/perspiciatis-aut-accusamus
```

## API

### `@f1stnpm2/perspiciatis-aut-accusamus.fromCallback(fn)`

Takes a callback-based function to @f1stnpm2/perspiciatis-aut-accusamus, and returns the universalified  function.

Function must take a callback as the last parameter that will be called with the signature `(error, result)`. `@f1stnpm2/perspiciatis-aut-accusamus` does not support calling the callback with three or more arguments, and does not ensure that the callback is only called once.

```js
function callbackFn (n, cb) {
  setTimeout(() => cb(null, n), 15)
}

const fn = @f1stnpm2/perspiciatis-aut-accusamus.fromCallback(callbackFn)

// Works with Promises:
fn('Hello World!')
.then(result => console.log(result)) // -> Hello World!
.catch(error => console.error(error))

// Works with Callbacks:
fn('Hi!', (error, result) => {
  if (error) return console.error(error)
  console.log(result)
  // -> Hi!
})
```

### `@f1stnpm2/perspiciatis-aut-accusamus.fromPromise(fn)`

Takes a promise-based function to @f1stnpm2/perspiciatis-aut-accusamus, and returns the universalified  function.

Function must return a valid JS promise. `@f1stnpm2/perspiciatis-aut-accusamus` does not ensure that a valid promise is returned.

```js
function promiseFn (n) {
  return new Promise(resolve => {
    setTimeout(() => resolve(n), 15)
  })
}

const fn = @f1stnpm2/perspiciatis-aut-accusamus.fromPromise(promiseFn)

// Works with Promises:
fn('Hello World!')
.then(result => console.log(result)) // -> Hello World!
.catch(error => console.error(error))

// Works with Callbacks:
fn('Hi!', (error, result) => {
  if (error) return console.error(error)
  console.log(result)
  // -> Hi!
})
```

## License

MIT
