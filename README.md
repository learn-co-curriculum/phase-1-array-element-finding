# Finding Array Elements

## Learning Goals

- Find elements using `Array.prototype.find()`
- Find elements using `Array.prototype.indexOf()`

## Introduction

| Use Case                                                       | Method                |
| -------------------------------------------------------------- | --------------------- |
| Executing a provided callback on each element                  | `forEach()`           |
| ** Finding a single element that meets a condition             | `find()`, `indexOf()` |
| Finding and returning a list of elements that meet a condition | `filter()`            |
| Modifying each element and returning the modified array        | `map()`               |
| Creating a summary or aggregation of values in an array        | `reduce()`            |

In the last lesson, we learned about the `forEach()` iterator method. In this
lesson we'll look at two iterator methods that help us locate data in arrays:
`Array.prototype.find()`, which can be used for a wide array of search
conditions, and `Array.prototype.indexOf()`, which can be used to search for a
specific value.

As you work through this lesson, you will notice that there is a lot of overlap
in how `forEach()` and `find()` work (`indexOf()` is a bit different). This will
be the case for all of the iterator methods you will learn about in this
module other than `indexOf()`. Specifically, they all:

1. iterate through the elements in the array they're called on,
2. take a callback as an argument,
3. automatically pass values to the callback, and
4. (with the exception of `forEach()`) return a value at the end.

All of them _except_ `reduce()` pass the same three values to the callback in
step 3 above: the current element, the index of the current element, and the
array itself. `reduce()` is a bit more complicated, but we'll get to that later.

## Find Elements Using `Array.prototype.find()`

`Array.prototype.find()` is called on an array and takes a callback function as
an argument. The method will automatically iterate through the array, call the
callback on each value, and return the first element in the array that satisfies
the condition defined by the callback. If no matching element is found,
`undefined` is returned.

In each iteration through the array, `Array.prototype.find()` passes three
arguments to the callback: the current element of the array, the index of the
current element, and the array itself. These arguments can then be captured as
parameters in the callback and used inside the function.

Say we want to determine whether an array of numbers contains any odd values. We
can write the following callback function to do this:

```js
function isOdd(element, index, array) {
  return element % 2 === 1;
}
```

`Array.prototype.find()` will iterate through the array it's called on, passing
the element (and the other two values) in turn to `isOdd()`. If the element is
not odd, the callback returns `false` and the iteration continues. If an odd
element is encountered, the callback will return `true`, and
`Array.prototype.find()` will return that element.

Remember that `Array.prototype.find()` _automatically_ passes the three
arguments to our function. By defining `isOdd()` with three parameters, we make
those values available inside our function. In this example, we're only using
the first one, the current element of the array, but all three are being passed
in and are available inside our function if we want to use them.

Let's call `.find()` on the array we want to search, and pass our function as an
argument:

```js
function isOdd(element, index, array) {
  return element % 2 === 1;
}

[4, 6, 8, 10].find(isOdd); //=> undefined, not found
[4, 5, 8, 10].find(isOdd); //=> 5
[4, 5, 7, 8, 10].find(isOdd); //=> 5
[4, 7, 5, 8, 10].find(isOdd); //=> 7
```

Let's walk through what's happening here, using the last example:

1. We call `.find()` on the array `[4, 7, 5, 8, 10]` and pass the `isOdd()`
   function as an argument.
2. The `.find()` method calls the callback and passes it the three arguments, in
   this case `4`, `0`, and the array itself.
3. `isOdd()` checks whether the current element is odd. It isn't, so it returns
   `false`.
4. `.find()` continues to the next element in the array and calls the callback
   again, passing it the new set of arguments.
5. `isOdd()` checks whether the current element (7) is odd and returns `true`.
6. `.find()` returns the current element and ends execution.

Note that in this case only the first argument — the current element in the
array — is required for the callback function. Recall from the last lesson that,
if (as in our example above) your callback doesn't use the other two arguments,
you can define your function with only the first parameter. This will work as
well:

```js
function isOdd(element) {
  return element % 2 === 1;
}
```

The ability to pass a callback function to `.find()` makes the method very
versatile. Anything you can program that returns a Boolean value can be used as
the search condition: a number greater than or less than a certain value, a
value of a certain data type, a word that begins with a vowel — the sky's the
limit! But sometimes you just need to determine whether a particular value is
present in the array. In this case, `Array.prototype.indexOf()` will save you
some work.

## Find Elements Using a Simple Condition with `Array.prototype.indexOf()`

If you need to search an array for a value, `Array.prototype.indexOf()` is a
simpler option. It is called on an array and takes two arguments: the value you
are looking for and an optional start position — no need to write a callback
function! It compares each element in turn to the value you're looking for using
the strict equality operator (`===`) and returns the index of the first matching
element. If the element isn't contained in the array, it returns -1.

```js
const cards = [
  "queen of hearts",
  "jack of clubs",
  "ten of diamonds",
  "ace of spades",
];

cards.indexOf("jack of clubs"); //=> 1
cards.indexOf("jack of hearts"); //=> -1
```

If you pass in the optional second argument, `indexOf()` will begin the search
at the specified position:

```js
cards.indexOf("ace of spades", 2); //=> 3
cards.indexOf("jack of clubs", 2); //=> -1
```

In this case, `Array.prototype.indexOf()` returns `-1` if either the value isn't
found _or_ if the start position you pass in is after the element you're looking
for.

**Challenge:** For practice, let's consider how we could use the `find()` method
rather than `indexOf()` to find a specific value, say, "king of diamonds".

<details><summary><b>What would the callback function be?</b></summary>
<code>function isKingOfDiamonds(element) {</code><br/>
<code>return element === "king of diamonds"</code><br/>
<code>}</code>
</details>

<details><summary><b>What would `find()` return if the value is in the array?</b></summary>
<ul>
<li>'king of diamonds'</li>
</ul>
</details>

<details><summary><b>What would `find()` return if the value isn't in the array?</b></summary>
<ul>
<li>undefined</li>
</ul>
</details>

## Conclusion

Both `Array.prototype.indexOf()`and `Array.prototype.find()` can be very useful
in different situations. `Array.prototype.indexOf()` is used when you want to
check an array for a simple value; you call `indexOf()` on an array, passing the
value you're looking for as the argument. `Array.prototype.find()` is also
called on an array, but it takes a _function_ as an argument. This enables you
to define the condition the element should meet, allowing for more complex
searches.

## Resources

- [Object.prototype](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)
- [Array.prototype.indexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
- [Array.prototype.find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
