# Higher-Order Functions

## Function can be treated as a variable

```js
function add(a, b) {
  return a + b;
}

// Store function to variable
let addFunc = add;
console.log(add(1, 2)); // 3
console.log(addFunc(1, 2)); // 3
console.log(addFunc === add); // true

// Store function to array
let funcArray = [add];
console.log(funcArray[0](1, 2)); // 3

// Store function to object
let funcObj = {
  add: add,
  //   add, <- You can use this syntax, If the property and the variable name is same.
};
console.log(funcObj.add(1, 2)); // 3
```

## Write Higher-Order functions to make more abstract

```js
function logNumbers() {
  for (let i = 0; i < 10; i++) {
    console.log(i);
  }
}

logNumbers(); // 0 1 2 ... 9
```

Write abstract code for above.

```js
function logNumbers(min, max) {
  for (let i = min; i < max; i++) {
    console.log(i);
  }
}

logNumbers(0, 10); // 0 1 2 ... 9
```

Write more abstract code using higher-order functions.

```js
function each(array, action) {
  for (let item in array) {
    action(item);
  }
}

function range(max) {
  // How [...Array(n).keys()] works
  // First, Array(n) will return [empty, empty, ... , empty]
  // empty mean that returned array does not even own a property
  //    let arr = Array(10);
  //    arr.length -> 10
  //    arr[0] -> undefined
  //    arr.hasOwnProperty("0") -> false
  // Second, Array(n).keys() will return the ITERATOR array of indexes in the array
  //    let iterator = Array(3).keys();
  //    iterator.next(); // Object { value: 0, done: false }
  //    iterator.next(); // Object { value: 1, done: false }
  //    iterator.next(); // Object { value: 2, done: false }
  // Last, ... operator will destruct the iterator array
  //    [...Array(n).keys()] -> [0, 1, 2]
  return [...Array(max).keys()];
}

each(range(10), console.log); // 0 1 2 ... 9
```
