# Array Element Finding

## Learning Goals

- Use `Array.prototype.indexOf()` to find elements in a simple array
- Use `Array.prototype.find()` to find elements in a more complex array

## Introduction

As developers, one of the things that we are asked to do on a regular basis is to locate things in in array. It's all well and good to be able to store data as developers, but it's pretty useless unless we're able to get it back out again. Being able to locate the right data is a crucial skill. In JavaScript, there are two different methods that we use to locate data in arrays. For a more simple solution, we use `Array.prototype.indexOf()`. For more complex calculations, we use `Array.prototype.find()`. In this lab, we will practice using both. 

## Use `Array.prototype.indexOf()` to Find Elements In an Array

`Array.prototype.indexOf()` depends on one required parameter, and one optional parameter. It compares the elements using the strict equality operator (===) and returns the index of the matching element. 

```js

let cards = ['queen of hearts', 'jack of clubs', 'ten of diamonds', 'ace of spades'];

console.log(cards.indexOf('jack of clubs')); //1

```

The first parameter, the _item_ that you are looking for, is required. You can also pass in the _start_ position like so:

```js

let cards = ['queen of hearts', 'jack of clubs', 'ten of diamonds', 'ace of spades'];

console.log(cards.indexOf('jack of clubs', 2  )); // -1 

```

However, if you pass in a start position that is after the element that you're looking for, or if the element that you are looking for is not in the array, `Array.prototype.indexOf()` will return `-1` to let you know. 

## Use `Array.prototype.find()` to Find Elements in a More Complex Array

`Array.prototype.find()` refers to a function to execute on each value in the array, taking in three arguments. 

```js

function isOdd(element, index, array) {
  return (element %2 === 1);
}

console.log([4, 6, 8, 10].find(isOdd)); // undefined, not found
console.log([4, 5, 8, 10].find(isOdd)); // 5
console.log([4, 5, 7, 8, 10].find(isOdd)); // 5
console.log([4, 7, 5,  8, 10].find(isOdd)); // 7
```

`Array.prototype.find()` takes in the element we'd like to find, the index at which we'd like to start, and the array, and returns the first element in the array satisfies the condition specifies the condition specified by the function. 


## Conclusion

As you can see, both `Array.prototype.indexOf()`and `Array.prototype.find()` can be very useful in different situations. With practice, you can become comfortable using them in any situation!

## Resources
[Array.prototype.indexOf()]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf
[Array.prototype.find()]: