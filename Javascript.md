# Javascript Cheat Sheet

## ES6

- let
- const
- arrow functions () => {}
- spread operator (...)
- rest parameter (...)
- destructuring
- classes and interfaces

## Variables

- var - global and function scoped, not block scoped (can be used outside of block it was declared in)
- let - block scoped, cannot be used in any higher block
- const - constant value

## Functions

```
function foo() {
  console.log('no params');
}

function printWord(word) {
  console.log(word);
}

function defaultWord(word = 'foo') {
  console.log(word);
}
```

## Arrow Functions

```
const add = (a, b) => {
  return a + b;
};

// concise
const add = (a, b) => a + b;

// 1 param
const printString = phrase => console.log(phrase);

const button = document.querySelector('button');
button.addEventListener('click', event => console.log(event));

```

## Spread Operator

```
const hobbies = ['Sports', 'Hiking'];
const activeHobbies = ['Hiking'];
activeHobbies.push('Camping')
activeHobbies.push(hobbies[0], hobbies[1]);
activeHobbies.push(...hobbies);  // spread operator

const moreHobbies = ['Hiking', ...hobbies];

const person = {
  name: 'Max',
  age: 30
};

const pointerToPerson = person;
const copiedPerson = {...person};
```

## Rest Parameter

```
const add = (...numbers) => {
  let result = 0;
  for (num in numbers) {
    result += num;
  }
  return result;
};

const add = (...numbers) => {
  return numbers.reduce((curResult, curValue) => {
    return curResult + curValue;
  }, 0);
};

const result = add(5, 10, 15, 2.3);
```

## Destructuring

array desctructuring:

```
const hobbies = ['Sports', 'Hiking', 'Camping'];

// by order in list
const [hobby1, hobby2, ...otherHobbies] = hobbies;
```

object desctructuring:

```
const person = {
  name: 'Max',
  age: 30,
  gender: 'Male'
};

// by property name
const { name, age } = person;

// change variable name it is stored in
const { name: firstName, age } = person;
console.log(firstName);
```

## Classes and Interfaces

All the beauty of Java (well most of it). Depends on JS version (use typescript).

```
class User {

  constructor(name) {
    this.name = name;
  }

  describe() {
    return 'User: ' + this.name;  // "this" refers to the calling object
  }
}

const user1 = new User('Gary');
console.log(user1.describe());
```

## Useful Links

- [ECMAScript 6 Compatability](https://compat-table.github.io/compat-table/es6/)
