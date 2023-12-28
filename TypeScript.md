# Typescript

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

### variables:

```
let myString: string = 'abc';
let myNumber: number = 10;
let myTruth: boolean = true;
let myNumbersArray: number[] = [1, 2, 3];
let myRandomArray: (string | number)[] = ['a', 2];
let noIdeaWhat = unknown;  // better than "any", will throw error if assigned where type req
```

### tuples and enums

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

### objects:

```
const person = {
  name: string;
  age: number;
}
```

### literal types and type aliases

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

### functions

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

## TSC Compilar

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
