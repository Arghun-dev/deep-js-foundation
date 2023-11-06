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
