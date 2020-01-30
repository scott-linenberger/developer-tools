# Javascript In The Wild

- Destructuring Assignment
- Arrow Functions
- Guards & Defaults
- Default Parameters
- Currying
- Spread Operator
- Rest parameters
- Ternaries

## [Destructuring Assignment][destructuring]

MDN Web Docs:

> The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

Destructuring has become the de facto standard for getting variables out of objects. Array destructuring is also quickly becoming a common sight. You may have already encountered array destructuring if you've used or seen [React hooks][react_hooks];

If you haven't seen destructuring before, it can be a little confusing.

```javascript
// consider this object
const person = {
  name: "Scott Linenberger",
  occupation: "Developer",
  address: {
    city: "Seattle",
    state: "WA"
  }
};

// using the object
console.log(
  `Hello, I'm ${person.name} and I live in ${person.address.city}, ${person.address.state}`
);

// assigning variables
const name = person.name;
const city = person.address.city;
const state = person.address.state;

console.log(`Hello, I'm ${name} and I live in ${city}, ${state}`);

// destructured object
const {
  name,
  address: { city, state }
} = person;

console.log(`Hello, I'm ${name} and I live in ${city}, ${state}`);

// consider this array
const arrayOfItems = ["Scott", "Seattle", "WA"];

// using the array
console.log(
  `Hello, I'm ${arrayOfItems[0]} and I live in ${arrayOfItems[1]}, ${arrayOfItems[2]}`
);

// assigning variables
const name = arrayOfItems[0];
const city = arrayOfItems[1];
const state = arrayOfItems[2];

console.log(`Hello, I'm ${name} and I live in ${city}, ${state}`);

// destructured array
const [name, city, state] = arrayOfItems;

console.log(`Hello, I'm ${name} and I live in ${city}, ${state}`);
```

## [Arrow Functions][arrow_functions]

MDN Web Docs:
> An arrow function expression is a syntactically compact alternative to a regular function expression, although without its own bindings to the this, arguments, super, or new.target keywords. Arrow function expressions are ill suited as methods, and they cannot be used as constructors.

Arrow functions are a great short-hand for writing functions.

```javascript
// consider this object
const person = {
  name: "Scott Linenberger",
  occupation: "Developer",
  address: {
    city: "Seattle",
    state: "WA"
  }
};

// traditional functions
const getCity = function(person) {
  return person.address.city;
};

function getCity(person) {
  return person.address.city;
}

// arrow function with a concise body
const getCity = person => person.address.city;

// arrow function with a block body
const getCity = person => {
  return person.address.city;
};

// arrow functions are great for Array.prototype functions

// consider the array of items
const arrayItems = [
  {
    name: "Rick"
  },
  {
    name: "Morty"
  },
  {
    name: "Jerry"
  }
];

// Array.prototype.find() with function
const rick = arrayItems.find(function(item) {
  return item.name === "Rick";
});

// Array.prototype.find() with arrow function using concise body
const rick = arrayItems.find(item => item.name === "Rick");

// Array.prototype.find() with arrow function with block body
const rick = arrayItems.find(item => {
  return item.name === "Rick";
});

// arrow functions with a single parameter are often written without parenthesis
const getName = person => person.name;

// parenthesis are often recommended. I prefer parenthesis
const getName = person => person.name;

// arrow functions can take more than a single parameter
// and arrow functions can have more logic
const compareNameLength = (person1, person2) => {
  const nameLengthPerson1 = person1.name.length;
  const nameLengthPerson2 = person2.name.length;

  // equal length
  if (nameLengthPerson1 === nameLengthPerson2) {
    return 0;
  }

  if (nameLengthPerson1 > nameLengthPerson2) {
    return 1;
  }

  return -1;
};

// I prefer vertical formatting for multiple parameters
const compareNameLength = (
  person1,
  person2,
) => {
  // ...
};
```

## [Guards and Defaults or "Short-circuit evaluation"][operators]

MDN Web Docs:

> As logical expressions are evaluated left to right, they are tested for possible "short-circuit" evaluation using the following rules:

> false && anything is short-circuit evaluated to false.
> true || anything is short-circuit evaluated to true.

> The rules of logic guarantee that these evaluations are always correct. Note that the anything part of the above expressions is not evaluated, so any side effects of doing so do not take effect.

If you've never seen a short-circuit evaluation (commonly called a "guard" or "default"), it can be a little confusing.

```javascript
// consider an object of this shape
const person = {
  name: "Scott Linenberger",
  occupation: "Developer",
  address: {
    city: "Seattle",
    state: "WA"
  }
};

// if you are trying to get a nested value, like city..
// this expression will throw an exception if address is undefined
const name = person.address.city;

// using a short-circuit guard, we can "guard" against undefined values
const name = person && person.address && person.address.city;

// I prefer vertical formatting
const name = person && peron.address && person.address.city;

// what if we wanted to assign a default address if one doesn't exist
// this short-circuit "default" will use person.address or the default
// value after the `||` operator if person.address is not defined.
const address = person.address || { city: "Seattle", state: "WA" };
```

[destructuring]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
[react_hooks]: https://reactjs.org/docs/hooks-intro.html
[arrow_functions]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions
[operators]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators
