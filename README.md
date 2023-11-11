# deep-js-foundation

```js
var x = 40;

x++;      // 40   --> after increment --> it gives you the value and then increments
x;        // 41


++x;      // 42   --> pre increment --> does the updating first and then returns the value 
x;        // 42
```

```js
var x = "5";

x = x + 1;    // "51"


var y = "5"; 

y++;    // 5    --> this goes ahead and coerce the "5" to a number first and then increments it 
y;      // 6
```


### ++ Definition

```js
// x++ means:

function plusplus(x) {
  const coercedX = Number(x);
  x = coercedX + 1;
  return coercedX;
}

var x = "5";
plusplus(x);  // 5
x;            // 6
```


## Course Overview


### Types

  . Primitive Types
  . Abstract Operations
  . Coercion
  . Equality
  . TypeScript, Flow, etc.

### Scope

  . Nested Scope
  . Hoisting
  . Closure
  . Modules

### Objects (Oriented)

  . this
  . class {}
  . Prototypes
  . OO vs. OLOO

`object`, `function`, `array` -> objects

`undfined`, `string`, `number`, `null`, `boolean`, `symbol` not object

in JavaScript `NaN` is the only value that is not equal to itself.

```js
NaN === NaN     // false
```

`isNaN` always coerce the value inside of the the function to a number and then see if it is nan or not.

```js
typeof NaN      // number
```


### Object.is

The `Object.is()` static method determines whether two values are the same value

```js
// Case 1: Evaluation result is the same as using ===
Object.is(25, 25); // true
Object.is("foo", "foo"); // true
Object.is("foo", "bar"); // false
Object.is(null, null); // true
Object.is(undefined, undefined); // true
Object.is(window, window); // true
Object.is([], []); // false
const foo = { a: 1 };
const bar = { a: 1 };
const sameFoo = foo;
Object.is(foo, foo); // true
Object.is(foo, bar); // false
Object.is(foo, sameFoo); // true

// Case 2: Signed zero
Object.is(0, -0); // false
Object.is(+0, -0); // false
Object.is(-0, -0); // true

// Case 3: NaN
Object.is(NaN, 0 / 0); // true
Object.is(NaN, Number.NaN); // true
```

example:

```js
function formatTrend(trendRate) {
  var direction = (direction < 0 || Object.is(trendRate, -0)) ? "decreasing" : "increasing";
  return `${direction} ${Math.abs(trenRate)}`;
}
```


### Define polyfill Object.is functino

```js
if (!Object.is) {
  Object.is = function ObjectIs(x, y) {
    let xNegZero = isItNegZero(x);
    let yNegZero = isItNegZero(y);

    if (xNegZero || yNegZero) {
      return xNegZero && yNegZero;
    }

    else if (isItNaN(x) && isItNaN(y)) {
      return true
    }

    else {
      return x === y;
    }
  }


  // *********************

  function isItNegZero(v) {
    return v == 0 && (1/v) == -Infinity;
  }

  function isItNaN(v) {
    return v !== v;
  }
}
```


### Fundamental Objects

Use `new`:

  . Object()
  . Array()
  . Function()
  . Date()
  . RegExp()
  . Error()

Don't use `new`:

  . String()
  . Number()
  . Boolean()


### Avoid these:

1. == with 0 or "" (or even "  ")
2. == with non-primitive
3. == true or == false: allow to Boolean or use ===


### The case for preferring ==

You should prefer == in all possible cases 

Knowing types is always bettern than not knowing them.

Static Types is `not` the only (or even necessarily best) way to know your types

`==` is `not` about comparison with unkown types => `Never` use the `==` when you don't know the types. Only use the `==` when you know the types.

`==` is about comparisons with known types, `optionally` where conversions are helpful.


Since === is pointless when the types don't match. => It's similarly `unnecessary` when they do match.


If you `know` the types in a comparison:

If the types are different, using one === would be broken.

Prefrer the `more powerful` == or `don't compare` at all.


Summary: if you `can't or won't` use known and obvious types, `===` is the only `reasonable` choice. But it's better you to `know` the types.
