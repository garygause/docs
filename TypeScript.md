# Typescript

- [Typescript](#typescript)
  - [Types](#types)
  - [Type Annotations](#type-annotations)
    - [Variables:](#variables)
    - [Tuples and Enums](#tuples-and-enums)
    - [Objects:](#objects)
    - [Literal Types and Type Aliases](#literal-types-and-type-aliases)
    - [Functions](#functions)
  - [Classes and Interfaces](#classes-and-interfaces)
    - [Inheritance:](#inheritance)
    - [Protected:](#protected)
    - [Getters and Setters:](#getters-and-setters)
    - [Static Methods and Properties:](#static-methods-and-properties)
    - [Abstract Classes and Interfaces](#abstract-classes-and-interfaces)
    - [Singletons](#singletons)
  - [Advanced Types](#advanced-types)
    - [Intersection Types](#intersection-types)
    - [Type Guards](#type-guards)
    - [Discriminated Unions](#discriminated-unions)
    - [Type Casting](#type-casting)
    - [Index Properties](#index-properties)
    - [Function Overloads](#function-overloads)
    - [Optional Chaining](#optional-chaining)
    - [Nullish Coalescing](#nullish-coalescing)
  - [Generics](#generics)
  - [Decorators](#decorators)
  - [TSC Compiler](#tsc-compiler)
    - [tsconfig](#tsconfig)

## Types

- number
- string
- boolean
- object
- never
- void
- any

- arrays: number[], string[]

## Type Annotations

Inferred types are preferred where possible.

i.e.

`let myString = 'abc';`

is preferred to:

`let myString: string = 'abc';`

### Variables:

```
let myString: string = 'abc';
let myNumber: number = 10;
let myTruth: boolean = true;
let myNumbersArray: number[] = [1, 2, 3];
let myRandomArray: (string | number)[] = ['a', 2];
let noIdeaWhat = unknown;  // better than "any", will throw error if assigned where type req
```

### Tuples and Enums

Purely typescript concept (at least in javascript land).

tuple:

```
let role: [number, string] = [0, 'ADMIN'];
```

enum:

replaces

```
const ADMIN = 0;
const READ_ONLY = 1;
const AUTHOR = 2;
```

with

```
// Role is a custom type.  custom types start with capitols.
// behind the scenes this defaults to 0, 1, 2 for values

enum Role { ADMIN, READ_ONLY, AUTHOR };

let myRole = Role.ADMIN;

// change start counter so values are 5, 6, 7
enum Role { ADMIN = 5, READ_ONLY, AUTHOR };

// all custom values
enum Role { ADMIN = 5, READ_ONLY = 100, AUTHOR = 'AUTHOR' };
```

### Objects:

```
const person = {
  name: string;
  age: number;
}
```

### Literal Types and Type Aliases

```
// literal types
const person: {
  name: string;
  age: number;
  role: 'ADMIN' | 'READ_ONLY' | 'AUTHOR';
}

// type aliases

type RoleDescriptor = 'ADMIN' | 'READ_ONLY' | 'AUTHOR';
const person: {
  name: string;
  age: number;
  role: RoleDescriptor;
}

type Combinable = number | string;
function combine(input1: Combinable, input2: Combinale) {
  return input1 + input2;
}

type User = { name: string; age: number };
const user1: User = {name: 'Gary', age: 54 };
function greetUser(user: User) {
  console.log("Hello, " + user.name);
}
```

### Functions

params:

```
function sayPhrase(phrase: string) {
  console.log(phrase);
}

function add(n1: number, n2: number) {
  return n1 + n2;
}

function logValue(myValue: string | number) {
  console.log(myValue);
}

```

return values:

```
function sayPhrase(phrase: string): void {
  console.log(phrase);
}

function add(n1: number, n2: number): number {
  return n1 + n2;
}

function throwError(error: string, code: number): never {
  throw { message: error, errorCode: code};
}

```

functions as types:

```
let combineValues: Function;

let combineValues: (a: number, b: number) => number;

function add(n1: number, n2: number): number {
  return n1 + n2;
}

combineValues = add;
combineValues(1, 2);
```

callbacks:

```
function addAndHanle(n1: number, n2: number, cb: (result: number) => void) {
  const result = n1 + n2;
  cb(result);
}

addAndHandle(1, 2, (result: number) => {
  console.log(result);
});

// callback can return even if void is the return value in function annotation
// annotation only means the function processing the callback will not use return value
addAndHandle(1, 2, (result: number) => {
  console.log(result);
  return result;
});
```

## Classes and Interfaces

```
class User {
  private id: string;
  name: string;
  public age: number;  // public is default, not needed
  private passwords: string[] = [];

  constructor(name: string) {
    this.name = name;
  }

  describe() {
    return 'User: ' + this.name;
  }

  // this is valid in typescript as well to be more strict
  describe2(this: User) {
    return 'User: ' + this.name;
  }

  addPassword(password: string) {
    this.passwords.push(password);
  }

  getPasswords() {
    return this.passwords;
  }

}

const user1 = new User('Gary');
console.log(user1.describe());
```

shortcut initialization (dont need to define fields):

```
class User {
  private passwords: string[];

  // id is set to readonly and private
  constructor(private readonly id: string, public name: string) {
    this.passwords = [];
  }

  describe() {
    return `User ${this.id}: ${this.name}`;
  }
}
```

optional properties:

```
class User {
  id: string;
  name?: string;

  constructor(n?: string) {
    if (n) {
      this.name = n;
    }
  }
}
```

### Inheritance:

```
class AdminUser extends User {
  private permissions: string[];

  constructor(id: string, name: string, permissions: string[]) {
    super(id, name);
    this.permissions = permissions;
  }
}
```

### Protected:

```
class User {
  protected passwords: string[];

  // id is set to readonly and private
  constructor(private readonly id: string, public name: string) {
    this.passwords = [];
  }

  describe() {
    return `User ${this.id}: ${this.name}`;
  }
}

class AdminUser extends User {
  private permissions: string[];

  constructor(id: string, name: string, permissions: string[]) {
    super(id, name);
    this.permissions = permissions;
    this.passwords = ['1234'];  // accessible because of protected keyword on parent
    this.id = '123';  // not accessible due to private keyword on parent
  }
}
```

### Getters and Setters:

```
class AdminUser extends User {
  private permissions: string[];

  constructor(id: string, name: string, permissions: string[]) {
    super(id, name);
    this.permissions = permissions;
  }

  get userPermissions() {
    return this.permissions;
  }

  set userPermissions(permissions: string[]) {
    this.permissions = permissions;
  }

}

const admin = new AdminUser('123', 'Gary', ['read', 'write']);
console.log(admin.userPermissions);
admin.userPermissions = ['read'];
```

### Static Methods and Properties:

```
class User {
  protected passwords: string[];
  static version = '1.0';

  // id is set to readonly and private
  constructor(private readonly id: string, public name: string) {
    this.passwords = [];
  }

  describe() {
    return `User ${this.id}: ${this.name}`;
  }

  static sayHello() {
    return 'Hello!';
  }

}

console.log(User.sayHello());
console.log(User.version);
```

### Abstract Classes and Interfaces

abstract classes can have implemented methods, unlike interfaces.

```
abstract class User {
  abstract id: string;
  abstract describe(): string;

  say(phrase: string) {
    console.log(phrase);
  }
}
```

interfaces:

```
interface PersonInterface {
  readonly id: string;
  name: string;
  age: number;
  describe(): string;
  say(phrase: string): void;
}

// object implementation
let person1: PersonInterface;
person1 = {
  name: 'Gary',
  age: 30,
  describe() {
    return `Person: ${this.name}``;
  },
  say(phrase: string) {
    console.log(phrase);
  }
}

// implements keyword
class Person implements PersonInterface {}

// can extend multiple interfaces
interface MultiInterface extends PersonInterface, Greetable {}

// interface as a function type
interface Adder {
  (a: number, b: number): number;
}
let add: Adder;

add = (n1: number, n2: number) => {
  return n1 + n2;
}

// optional properties
interface Named {
  readonly name: string;
  nickname?: string;  // optional property
}


```

interfaces can have readonly modifier, but not private or others.

### Singletons

Always only have one instance of a class, e.g. one db connection.

```
Class DB {
  db: string;
  private static instance: DB;

  private constructor() {
    this.db = 'example';
  }

  static getInstance() {
    if (DB.instance) {
      return this.instance;
    } else {
      this.instance = new DB();
      return this.instance;
    }
  }
}

const db = DB.getInstance();

```

## Advanced Types

### Intersection Types

Intersection types allow us to combine other types.

```
type Admin = {
  name: string;
  permissions: string[];
}

type User {
  name: string;
  startDate: Date;
}

type AdminUser = Admin & User;

const user1: AdminUser = {
  name: 'Gary',
  permissions: ['Read', 'Write'],
  startDate: new Date()
}

type Combinable = string | number;
type Numeric = number | boolean;
type Universal = Combinable & Numeric;  // number
```

Intersection of object types is all types, the union. Intersection of types, is what they have in common.

### Type Guards

Type guards help with union types.

```
type Combinable = string | number;
function add(a: Combinable, b: Combinable) {
  // the typeof expression is a type guard
  if (typeof a === 'string' || typeof b === string) {
    return a.toString() + b.toString();
  }
  return a + b;
}

type UnknownUser = Admin | User;
function checkPermissions(user: UnknownUser) {
  // type guard
  if ('permissions' in user) {
    console.log(user.permissions);
  }
}

// class type guard
class Car {
  driver() {
    console.log('driving');
  }
}

class Truck {
  drive() {
    console.log('driving');
  }
  loadCargo(amount: number) {
    console.log(amount);
  }
}

type Vehicle = Car | Truck;

const v1 = new Car();
const v2 = new Truck();

function useVehicle(vehicle: Vehicle) {
  vehicle.drive();
  // this works
  if ('loadCargo' in vehicle) {
    vehicle.loadCargo(100);
  }
  // better method for classes
  if (vehicle instanceof Truck) {
    vehicle.loadCargo(100);
  }
}
```

### Discriminated Unions

Pattern for working with union types. Makes implementing type guards easier. A discriminated union sets a property (type below) in each interface or type that allows us to discriminate which one we are using. A "safer" pattern for working with union types.

```
interface Bird {
  type: 'bird';
  flyingSpeed: number;
}

interface Horse {
  type: 'horse';
  groundSpeed: number;
}

type Animal = Bird | Horse;

function moveAnimal(animal: Animal) {
  let speed: number;
  switch (animal.type) {
    case 'bird':
      speed = animal.flyingSpeed;
      break;
    case 'horse':
      speed = animal.groundSpeed;
  console.log(speed);
  }
}
```

### Type Casting

Type casting helps us tell typescript that something is of a particular type. Very useful when working with the dom.

```
//alternate syntax
const paragraph = <HTMLParagraphElement></HTMLParagraphElement>document.queryElementById('main-paragraph')!;  // ! at end means ignore null check, ts does not know what html exists

const userInput = document.getElementById('user-input')! as HTMLInputElement;

// if we don't know if it will be null or not:
const userInput = document.getElementById('user-input');
if (userInput) {
  (userInput as HTMLInputElement).value = 'Enter something';
}
```

### Index Properties

Useful if we don't know what properties we will have or want to know.

```
interface ErrorContainer {
  // this means any property added to this must be a string and its value must be a string
  [prop: string]: string;  // 'email', 'username', etc
}

const errorBag: ErrorContainer = {
  email: 'not a valid email',
  username: 'must start with a character'
}
```

### Function Overloads

Similar in concept to other languages, but is used for return types to help typescript.

```
type Combinable = string | number;

// tells typescript the return type when multiple are possible
// must be right above main function

function add(a: number, b: number): number;
function add(a: string, b: string): string;
function add(a: string, b: number): string;
function add(a: number, b: string): string;
function add(a: Combinable, b: Combinable) {
  // the typeof expression is a type guard
  if (typeof a === 'string' || typeof b === string) {
    return a.toString() + b.toString();
  }
  return a + b;
}
```

### Optional Chaining

Useful when we don't know if a property is defined, e.g. when retrieving data from a database.

```
const fetchedData = {
  id: '123',
  name: 'Gary',
  job: { title: 'CTO', description: 'Big Boss' }
}

// let's say that data comes from the db or from a none typescript source
// manual method
console.log(fetchedData.job && fetchedData.job.title);

// typescript method
console.log(fetchedData?.job?.title);  // chaining
```

### Nullish Coalescing

Useful if we have data that we aren't sure if it is null-ish.

```
const data = userInput || 'Default';  // fails on ''
const data = userInput ?? 'Default';  // null-ish coalescing, checks for null or undefined
```

## Generics

## Decorators

## TSC Compiler

basic usage:

```
tsc file.ts  // creates file.js
```

watch file:

```
tsc file.ts -w // or --watch
```

create typescript project (creates `tsconfig.json`):

```
tsc --init
```

then when we run `tsc` it will compile all .ts files in directory. same for `tsc -w`, which will watch all .ts files for changes and compile.

### tsconfig

Configuration file for the tsc compiler.

exclude/include files:

```
  },
  "exclude": [
    "filename.ts",  // specific file
    "*.dev.ts",  // any file matching pattern
    "**/*.dev.ts",  // any file matching pattern in any folder
    "node_modules",  // excluded as default setting, so not necessary
  ],
  // include will skip all files not in this list (and remove exclude from this list)
  "include": [
    "app.ts"
  ]
}
```

important options:

- target: what javascript version to compile to
  - es5, es6 (es2015), es2016
  - in vscode ctl-space will show all options
- lib: libraries to include
  - when commented out, default libs are included
  - reasonable values (defaults for es6 target)
    - "dom"
    - "es6"
    - "dom.iterable"
    - "scripthost"
- allowJs: will compile .js files as well (leave commented out)
- checkJs: will check .js files for errors (leave commented out)
- declaration: creates type files for sharing modules
- sourceMap: useful for debugging
- outDir: directory to output compiled js to ("./dist")
- rootDir: directory where ts files can be found ("./src")
- removeComments: remove comments from ts files when compiling (optimization)
- noEmitOnError: do not create any .js files on error (if true), default false
