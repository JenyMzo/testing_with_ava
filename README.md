# Testing with AVA
A tutorial for write tests using AVA JS

**Before starting...**

1. Install [Node.js](http://nodejs.org/)
2. Create a project folder and run `npm init`
3. Fill the package.json fields
4. Run `npm install --save-dev ava`
5. Run `ava --init` to add AVA to the package.json
6. Create a file `index.js` 
7. Create a folder called tests with a `.js` file inside.
8. Create a script on your package.js `"test": "ava --verbose"

## Log the icon

Developing apps and modules is fun. However often you might be concerned whether
things work or when you add new features you want to be sure you did not break
anything. Therefore developers invented tests for their well-being. They allow 
you to automatically, well, test your application or module.

Let's assume you wrote a function called `shruglify`, which takes a String and
adds a space and a `¯\_(ツ)_/¯` to it. How would you check that your function is
working?

Maybe your first idea was calling the function with a value and `console.log`
the result and then check its output in the console.

```js
var shruglify = require('./shruglify.js');
console.log(shruglify('hello world'));
```
Try this yourself.

**Function**
```js
module.exports = function shruglify(word) {
	return word + ' ¯\_(ツ)_/¯';
}
```
-----

## Friday the 13th

Months That Begin on a Sunday will Always have a Friday the 13th

Write a test for the function `isFridayTheThirteen`, it will assure that function returns `true` when passing `sunday` in it.


### Hints

The `console.log()` statement is very useful when we want to know what's going on with our code. So, if a larger application depends on a specific function in many places, a small change in one place could create a hard to find a bug. NodeJS provide us `asserts`. A best way to control and monitoring the behavior of our code.

Let's see how it works...

```js
  var assert = require('assert');
  assert(add(2,1) === 3,'add(2,1) should be 3');
```

Or as alternatively:
```js
  assert.deepEqual(add(2,1), 3, 'add(2,1) should be 3');
```

Here are some functions you can use with assert. 
```js
assert.ok(value, message) // tests if value is truthy
assert.equal(actual, expected, message) // ==
assert.notEqual(actual, expected, message) // !=
assert.deepEqual(actual, expected, message) // for comparing objects
assert.notDeepEqual(actual, expected, message)
assert.strictEqual(actual, expected, message) // ===
assert.notStrictEqual(actual, expected, message) // !==
```

**Function**
```js
module.exports = function isFridayTheThirteen(day) {
  return day === 'sunday';
}
```
-----

## Pass this on

It's more funny writing code than testing code... :) 

The AVA structure is pretty simple. If we use ES6 especifications we can create a test using arrow functions

```js
  test('My first test using AVA', t => {
	  //Instructions
  });
```
Let's start writing a test that always passes. You can do that using:

```js
  t.pass();
```
-----

## Rocking with AVA

Write tests that output `TAP`, that tests the following properties of a function

1 `fancify(str)` returns the `str` wrapped in `~*~`
  Example: `fancify('Hello')` returns `~*~Hello~*~`
2 It takes an optional second argument that converts the string into ALLCAPS
  Example: `fancify('Hello', true)` returns `~*~HELLO~*~`
3 It takes a third optional argument that determines the character in the middle
  Example: `fancify('Hello', false, '!')` returns `~!~Hello~!~`

### Hints

Let's see a test example using AVA:

``` js 
  test('test #1', t => {
    t.is(index.getName(), 'Andromeda', 'it Works');
  });
```

Don't forget to get the source.
```js
  const test = require('ava');
```

Here is a list of some assertions you can use with AVA. 

```js
.pass([message]) //Passing assertion.
.fail([message]) //Failing assertion.
.truthy(value, [message]) //Assert that value is truthy.
.falsy(value, [message]) //Assert that value is falsy.
.true(value, [message]) //Assert that value is true.
.false(value, [message]) //Assert that value is false.
.is(value, expected, [message]) //Assert that value is the same as expected. This is based on Object.is().
.not(value, expected, [message])//Assert that value is not the same as expected. This is based on Object.is().
.deepEqual(value, expected, [message]) //Assert that value is deeply equal to expected. See Concordance for details. Works with React elements and react-test-renderer.
.notDeepEqual(value, expected, [message])//Assert that value is not deeply equal to expected. The inverse of .deepEqual().
```

#### Resources
- AVA documentation: https://www.npmjs.com/package/ava

**Function**
```js
module.exports = function fancify(str, allcaps, char) {
  if (allcaps) str = str.toUpperCase();
  char = char || '*';
  return '~' + char + '~' + str + '~' + char + '~';
}
```
-----

## Pizza time

Write a test for a function `pizzaMaker(n, cb)`, that calls the callback 
`cb` exactly `n` times. `n` can be any number you want in your test code.

### Hints

Sometimes we are not simply checking return values of functions.
For this resason, we often want
to know: Was that callback called or not?

If we need to finish with a test we can use:

`t.end()`

However there is maybe a better way to do this with callbacks using `t.plan(n)`.
When we call this in the beginning we can tell `AVA` how many times we are going to run an assert.

```js
test('nextTick', t => {
    t.plan(1);
    process.nextTick(function () {
      	t.pass('callback called');
    });
})
```

In this example we only have one callback, which will simply pass the test when
it is called. So we could have used `t.end()` within the callback instead like this.

```js
test.cb('testing with a callback', t => {
	callback('', t.end);
});
```

**Function**
```js
module.exports = function pizzaMaker = (n, cb) => {
  if (n < 1) {
    return cb(null, true);
  }
  return cb('error');
};
```
-----
## Looking for creatures

Write a test for a promise `lookingForCreatures()`, that verifies that promise is resolving with a `unicorn 🦄.`

When you are going to test if a promise is resolving you can do the following:

```js
test('Looking for creatures', t => {
	return anyPromise().then(res => {
		t.is(result, expected);
	});
});
```

Also there are another assertions to test promises

```js
.throws(promise, [error, [message]]) //Assert that `function` throws an error, or `promise` rejects with an error.
.notThrows(promise, [message]) //Assert that `function` does not throw an error or that `promise` does not reject with an error.
```

**Function**
```js
const lookingForCreatures = function lookingForCreatures() {
    return new Promise((resolve, reject) => {
        setTimeout(function(){
        resolve("unicorn 🦄");
        }, 250);
    });
};
```






