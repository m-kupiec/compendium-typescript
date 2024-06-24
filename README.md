# TypeScript Reference

## TOC

### Overview

- **Definition**
- **Benefits**
- **Installation**
- **Getting Started**

### Language

- **Types**
  - Primitive Types
    - Overview
    - `null`/`undefined`
    - `Object`/`{}`/`any`
  - Complex Types
    - Arrays
    - Promises
    - Objects
- **Type Definition**
  - Overview
  - Type Annotation
  - Interfaces vs. Type Aliases
  - Interface Declaration
    - Objects
    - Classes
    - Functions
  - Type Alias
- **Type Composition**
  - Overview
  - Unions
    - Overview
    - Type Narrowing
    - Non-Null Assertion Operator
  - Generics
- **Miscellaneous**
  - Type Assertion
  - Function Overload Signature
  - Modules
    - Importing Modules
    - Exporting from Modules
    - Using Libraries

### Type Checker

- **Overview**
- **Structural Type System**
- **Type Inference**
- **Configuration**
  - Strictness
    - Overview
    - `noImplicitAny`
    - `noImplicitThis`
    - `strictNullChecks`

### Compiler

- **Configuration**
- **Output**

# Overview

## Definition

"a strongly typed programming language" ([TypeScript](https://www.typescriptlang.org))

"uses type inference" ([TypeScript](https://www.typescriptlang.org))

"adds additional syntax to JavaScript" ([TypeScript](https://www.typescriptlang.org))

"Describe the shape of objects and functions in your code." ([TypeScript](https://www.typescriptlang.org))

## Benefits

"giving you better tooling at any scale" ([TypeScript](https://www.typescriptlang.org))

"to support a tighter integration with your editor. Catch errors early in your editor." ([TypeScript](https://www.typescriptlang.org))

"Making it possible to see documentation and issues in your editor." ([TypeScript](https://www.typescriptlang.org))

"uses type inference to give you great tooling without additional code." ([TypeScript](https://www.typescriptlang.org))

"Many JavaScript apps are made up of hundreds of thousands of files. A single change to one individual file can affect the behaviour of any number of other files, like throwing a pebble into a pond and causing ripples to spread out to the bank. Validating the connections between every part of your project can get time consuming quickly, using a type-checked language like TypeScript can handle that automatically and provide instant feedback during development. These features allows TypeScript to help developers feel more confident in their code, and save considerable amounts time in validating that they have not accidentally broken the project." ([TypeScript](https://www.typescriptlang.org/why-create-typescript/))

## Installation

Installing:

```bash
npm install typescript --save-dev
```

Running the compiler:

```bash
npx tsc index.ts
```

## Getting Started

"Visual Studio Code uses TypeScript under the hood to make it easier to work with JavaScript." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

> Adding this to a JS file shows errors in your editor:
>
> ```js
> // @ts-check
> ```
>
> [TypeScript](https://www.typescriptlang.org)

> Using JSDoc to give type information:
>
> ```js
> /** @param {any[]} arr */
> ```
>
> [TypeScript](https://www.typescriptlang.org)

# Language

## Types

### Primitive Types

#### Overview

"There is already a small set of primitive types available in JavaScript: `boolean`, `bigint`, `null`, `number`, `string`, `symbol`, and `undefined`, which you can use in an interface. TypeScript extends this list with a few more, such as `any` (allow anything), `unknown` (ensure someone using this type declares what the type is), `never` (it’s not possible that this type could happen), and `void` (a function which returns `undefined` or has no return value)." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

#### `null`/`undefined`

"By default, TypeScript assumes that `null` and `undefined` are in the domain of every type. That means anything declared with the type `number` could be `null` or `undefined`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"When `strictNullChecks` is enabled, `null` and `undefined` get their own types called `null` and `undefined` respectively." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

#### `Object`/`{}`/`any`

"You might be tempted to use `Object` or `{}` to say that a value can have any property on it . . . However `any` is actually the type you want to use in those situations, since it’s the most flexible type. For instance, if you have something that’s typed as `Object` you won’t be able to call methods like `toLowerCase()` on it. . . . `any` is special in that it is the most general type while still allowing you to do anything with it. That means you can call it, construct it, access properties on it, etc." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"whenever you use `any`, you lose out on most of the error checking and editor support that TypeScript gives you." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"If a decision ever comes down to `Object` and `{}`, you should prefer `{}`. While they are mostly the same, technically `{}` is a more general type than `Object` in certain esoteric cases." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

### Complex Types

#### Arrays

"you can use the syntax `number[]`; this syntax works for any type (e.g. `string[]` is an array of strings, and so on). You may also see this written as `Array<number>`, which means the same thing." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

#### Promises

> If you want to annotate the return type of a function which returns a promise, you should use the `Promise` type:
>
> ```ts
> async function getFavoriteNumber(): Promise<number> {
>   return 26;
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

#### Objects

"You can use `,` or `;` to separate the properties, and the last separator is optional either way." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

"The type part of each property is also optional. If you don’t specify a type, it will be assumed to be `any`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

> Object types can also specify that some or all of their properties are optional. To do this, add a `?` after the property name:
>
> ```ts
> function printName(obj: { first: string; last?: string }) {
>   // ...
> }
> // Both OK
> printName({ first: "Bob" });
> printName({ first: "Alice", last: "Alisson" });
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

"In JavaScript, if you access a property that doesn’t exist, you’ll get the value `undefined` rather than a runtime error. Because of this, when you read from an optional property, you’ll have to check for `undefined` before using it." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

## Type Definition

### Overview

"some design patterns make it difficult for types to be inferred automatically (for example, patterns that use dynamic programming). To cover these cases, TypeScript supports an extension of the JavaScript language, which offers places for you to tell TypeScript what the types should be." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

### Type Annotation

"Type annotations in TypeScript are lightweight ways to record the intended contract of the function or variable." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-tooling-in-5-minutes.html))

"If you’re starting out, try using fewer type annotations than you think - you might be surprised how few you need for TypeScript to fully understand what’s going on." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

"Much like variable type annotations, you usually don’t need a return type annotation because TypeScript will infer the function’s return type based on its `return` statements. . . . Some codebases will explicitly specify a return type for documentation purposes, to prevent accidental changes, or just for personal preference." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

> Anonymous functions are a little bit different from function declarations. When a function appears in a place where TypeScript can determine how it’s going to be called, the parameters of that function are automatically given types. . . .
>
> ```js
> const names = ["Alice", "Bob", "Eve"];
>
> // Contextual typing for function - parameter s inferred to have type string
> names.forEach(function (s) {
>   console.log(s.toUpperCase());
> });
>
> // Contextual typing also applies to arrow functions
> names.forEach((s) => {
>   console.log(s.toUpperCase());
> });
> ```
>
> Even though the parameter `s` didn’t have a type annotation, TypeScript used the types of the `forEach` function, along with the inferred type of the array, to determine the type `s` will have.
>
> This process is called _contextual typing_ because the _context_ that the function occurred within informs what type it should have.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

### Interfaces vs. Type Aliases

"there are two syntaxes for building types: Interfaces and Types. You should prefer `interface`. Use `type` when you need specific features." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

"For the most part, you can choose based on personal preference, and TypeScript will tell you if it needs something to be the other kind of declaration. If you would like a heuristic, use `interface` until you need to use features from `type`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

"Almost all features of an `interface` are available in `type`, the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

Limitations of interfaces:

- "Interfaces may only be used to declare the shapes of objects, not rename primitives." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

Limitations of type aliases:

- "Type aliases may not participate in declaration merging, but interfaces can." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))
- "Using interfaces with extends can often be more performant for the compiler than type aliases with intersections" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

### Interface Declaration

#### General

> Extending an interface:
>
> ```ts
> interface Animal {
>   name: string;
> }
>
> interface Bear extends Animal {
>   honey: boolean;
> }
>
> const bear = getBear();
> bear.name;
> bear.honey;
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

Adding new fields to an existing interface:

> ```ts
> interface Window {
>   title: string;
> }
>
> interface Window {
>   ts: TypeScriptAPI;
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

#### Objects

> You can explicitly describe this object’s shape using an interface declaration:
>
> ```ts
> interface User {
>   name: string;
>   id: number;
> }
> ```
>
> You can then declare that a JavaScript object conforms to the shape of your new >interface by using syntax like : TypeName after a variable declaration:
>
> ```ts
> const user: User = {
>   name: "Hayes",
>   id: 0,
> };
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

#### Classes

> You can use an interface declaration with classes:
>
> ```ts
> interface User {
>   name: string;
>   id: number;
> }
>
> class UserAccount {
>   name: string;
>   id: number;
>
>   constructor(name: string, id: number) {
>     this.name = name;
>     this.id = id;
>   }
> }
>
> const user: User = new UserAccount("Murphy", 1);
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

#### Functions

> You can use interfaces to annotate parameters and return values to functions:
>
> ```ts
> function deleteUser(user: User) {
>   // ...
> }
>
> function getAdminUser(): User {
>   //...
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

### Type Alias

"type alias is exactly that - a name for any type." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

> Note that aliases are _only_ aliases - you cannot use type aliases to create different/distinct “versions” of the same type. When you use the alias, it’s exactly as if you had written the aliased type. In other words, this code might look illegal, but is OK according to TypeScript because both types are aliases for the same type:
>
> ```ts
> type UserInputSanitizedString = string;
>
> function sanitizeInput(str: string): UserInputSanitizedString {
>   return sanitize(str);
> }
>
> // Create a sanitized input
> let userInput = sanitizeInput(getInput());
>
> // Can still be re-assigned with a string though
> userInput = "new input";
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

> Extending a type via intersections:
>
> ```ts
> type Animal = {
>   name: string;
> };
>
> type Bear = Animal & {
>   honey: boolean;
> };
>
> const bear = getBear();
> bear.name;
> bear.honey;
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

## Type Composition

### Overview

"TypeScript’s type system allows you to build new types out of existing ones using a large variety of operators." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

"you can create complex types by combining simple ones. There are two popular ways to do so: with unions, and with generics." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

### Unions

#### Overview

"A union type is a type formed from two or more other types, representing values that may be _any_ one of those types. We refer to each of these types as the union’s _members_." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

> With a union, you can declare that a type could be one of many types. . . .
>
> ```ts
> type MyBool = true | false;
> ```
>
> `MyBool` . . . is classed as `boolean`
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

> A popular use-case for union types is to describe the set of `string` or `number` literals that a value is allowed to be:
>
> ```ts
> type WindowStates = "open" | "closed" | "minimized";
> type LockStates = "locked" | "unlocked";
> type PositiveOddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

#### Type Narrowing

"Narrowing occurs when TypeScript can deduce a more specific type for a value based on the structure of the code." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

> Unions provide a way to handle different types too. For example, you may have a function that takes an `array` or a `string` . . . you can make a function return different values depending on whether it is passed a string or an array:
>
> ```ts
> function wrapInArray(obj: string | string[]) {
>   if (typeof obj === "string") {
>     return [obj];
>   }
>   return obj;
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

> TypeScript will only allow an operation if it is valid for _every_ member of the union. For example, if you have the union `string | number`, you can’t use methods that are only available on `string` . . . The solution is to _narrow_ the union with code . . . For example, TypeScript knows that only a `string` value will have a `typeof` value `"string"`:
>
> ```ts
> function printId(id: number | string) {
>   if (typeof id === "string") {
>     // In this branch, id is of type 'string'
>     console.log(id.toUpperCase());
>   } else {
>     // Here, id is of type 'number'
>     console.log(id);
>   }
> }
> ```
>
> Another example is to use a function like `Array.isArray`:
>
> ```ts
> function welcomePeople(x: string[] | string) {
>   if (Array.isArray(x)) {
>     // Here: 'x' is 'string[]'
>     console.log("Hello, " + x.join(" and "));
>   } else {
>     // Here: 'x' is 'string'
>     console.log("Welcome lone traveler " + x);
>   }
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

"Sometimes you’ll have a union where all the members have something in common. For example, both arrays and strings have a `slice` method. If every member in a union has a property in common, you can use that property without narrowing" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

#### Non-Null Assertion Operator

> If you ever have a value that TypeScript thinks is possibly `null`/`undefined`, but you know better, you can use the postfix `!` operator to tell it otherwise.
>
> ```ts
> declare var foo: string[] | null;
> foo.length; // error - 'foo' is possibly 'null'
> foo!.length; // okay - 'foo!' just has type 'string[]'
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

### Generics

"Generics provide variables to types." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

> An array with generics can describe the values that the array contains.
>
> ```ts
> type StringArray = Array<string>;
> type NumberArray = Array<number>;
> type ObjectWithNameArray = Array<{ name: string }>;
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

> You can declare your own types that use generics:
>
> ```ts
> interface Backpack<Type> {
>   add: (obj: Type) => void;
>   get: () => Type;
> }
>
> declare const backpack: Backpack<string>;
>
> // object is a string, because we declared it above as the variable part of Backpack.
> const object = backpack.get();
>
> // Since the backpack variable is a string, you can't pass a number to the add function.
> backpack.add(23);
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

## Miscellaneous

### Type Assertion

> ```js
> var options = {};
> options.color = "red";
> options.volume = 11;
> ```
>
> TypeScript will say that you can’t assign to `color` and `volume` because it first figured out the type of `options` as `{}` which doesn’t have any properties.
>
> . . . You could . . . define the type of `options` and add a type assertion on the object literal.
>
> ```ts
> interface Options {
>   color: string;
>   volume: number;
> }
>
> let options = {} as Options;
> options.color = "red";
> options.volume = 11;
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

### Function Overload Signature

> You’ll sometimes find yourself calling a function with too many/few arguments. Typically, this is a bug, but in some cases, you might have declared a function that uses the `arguments` object instead of writing out any parameters:
>
> ```js
> function myCoolFunction() {
>   if (arguments.length == 2 && !Array.isArray(arguments[1])) {
>     var f = arguments[0];
>     var arr = arguments[1];
>     // ...
>   }
>   // ...
> }
> myCoolFunction(
>   function (x) {
>     console.log(x);
>   },
>   [1, 2, 3, 4]
> );
> myCoolFunction(
>   function (x) {
>     console.log(x);
>   },
>   1,
>   2,
>   3,
>   4
> );
> ```
>
> In this case, we need to use TypeScript to tell any of our callers about the ways `myCoolFunction` can be called using function overloads.
>
> ```ts
> function myCoolFunction(f: (x: number) => void, nums: number[]): void;
> function myCoolFunction(f: (x: number) => void, ...nums: number[]): void;
> function myCoolFunction() {
>   if (arguments.length == 2 && !Array.isArray(arguments[1])) {
>     var f = arguments[0];
>     var arr = arguments[1];
>     // ...
>   }
>   // ...
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

### Modules

#### Importing Modules

"You might start out getting a bunch of errors like `Cannot find name 'require'.`, and `Cannot find name 'define'.`. In these cases, it’s likely that you’re using modules." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

> While you can just convince TypeScript that these exist by writing out
>
> ```ts
> // For Node/CommonJS
> declare function require(path: string): any;
> ```
>
> or
>
> ```ts
> // For RequireJS/AMD
> declare function define(...args: any[]): any;
> ```
>
> it’s better to get rid of those calls and use TypeScript syntax for imports.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

"First, you’ll need to enable some module system by setting TypeScript’s `module` option. Valid options are `commonjs`, `amd`, `system`, and `umd`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

> If you had the following Node/CommonJS code:
>
> ```js
> var foo = require("foo");
> foo.doStuff();
> ```
>
> or the following RequireJS/AMD code:
>
> ```js
> define(["foo"], function (foo) {
>   foo.doStuff();
> });
> ```
>
> then you would write the following TypeScript code:
>
> ```ts
> import foo = require("foo");
> foo.doStuff();
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

#### Exporting from Modules

"Typically, exporting from a module involves adding properties to a value like exports or module.exports. TypeScript allows you to use top-level export statements." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

> if you exported a function like so:
>
> ```js
> module.exports.feedPets = function (pets) {
>   // ...
> };
> ```
>
> you could write that out as the following:
>
> ```ts
> export function feedPets(pets) {
>   // ...
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

> Sometimes you’ll entirely overwrite the exports object. This is a common pattern people use to make their modules immediately callable like in this snippet:
>
> ```js
> var express = require("express");
> var app = express();
> ```
>
> You might have previously written that like so:
>
> ```js
> function foo() {
>   // ...
> }
> module.exports = foo;
> ```
>
> In TypeScript, you can model this with the `export =` construct.
>
> ```ts
> function foo() {
>   // ...
> }
> export = foo;
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

#### Using Libraries

"If you started converting over to TypeScript imports, you’ll probably run into errors like `Cannot find module 'foo'.`. The issue here is that you likely don’t have declaration files to describe your library." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"If TypeScript complains about a package like `lodash`, you can just write `npm install -S @types/lodash`" ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"If you’re using a module option other than `commonjs`, you’ll need to set your `moduleResolution` option to `node`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

# Type Checker

## Overview

"The goal of TypeScript is to be a static typechecker for JavaScript programs - in other words, a tool that runs before your code runs (static) and ensures that the types of the program are correct (typechecked)." ([TypeScript](https://www.typescriptlang.org/docs/handbook/intro.html))

## Structural Type System

"One of TypeScript’s core principles is that type checking focuses on the shape that values have. This is sometimes called “duck typing” or “structural typing”. In a structural type system, if two objects have the same shape, they are considered to be of the same type." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

"If the object or class has all the required properties, TypeScript will say they match, regardless of the implementation details." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

"In TypeScript, objects are _not_ of a single exact type. For example, if we construct an object that satisfies an interface, we can use that object where that interface is expected even though there was no declarative relationship between the two. . . . TypeScript’s type system is _structural_, not nominal" ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html))

"TypeScript’s type system is also not _reified_: There’s nothing at runtime that will tell us that `obj` is `Pointlike`. In fact, the `Pointlike` type is not present in any form at runtime." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html))

"In C# or Java, it’s meaningful to think of a one-to-one correspondence between runtime types and their compile-time declarations. In TypeScript, it’s better to think of a type as a set of values that share something in common. Because types are just sets, a particular value can belong to many sets at the same time. . . . we can think of `obj` as being a member of both the `Pointlike` set of values and the `Named` set of values." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html))

## Type Inference

"TypeScript knows the JavaScript language and will generate types for you in many cases. For example in creating a variable and assigning it to a particular value, TypeScript will use the value as its type." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

> For example, to create an object with an inferred type which includes `name: string` and `id: number`, you can write:
>
> ```js
> const user = {
>   name: "Hayes",
>   id: 0,
> };
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)

"Point-free programming — heavy use of currying and function composition — is possible in JavaScript, but can be verbose. In TypeScript, type inference often fails for point-free programs, so you’ll end up specifying type parameters instead of value parameters. The result is so verbose that it’s usually better to avoid point-free programming." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html))

## Configuration

### Strictness

#### Overview

"a lot of users prefer to have TypeScript validate as much as it can straight away, and that’s why the language provides strictness settings as well. . . . The further you turn this dial up, the more TypeScript will check for you. This can require a little extra work, but generally speaking it pays for itself in the long run, and enables more thorough checks and more accurate tooling." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/basic-types.html))

"When possible, a new codebase should always turn these strictness checks on." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/basic-types.html))

"TypeScript has several type-checking strictness flags that can be turned on or off, and all of our examples will be written with all of them enabled unless otherwise stated. The `strict` flag in the CLI, or `"strict": true` in a `tsconfig.json` toggles them all on simultaneously, but we can opt out of them individually. The two biggest ones you should know about are `noImplicitAny` and `strictNullChecks`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/basic-types.html))

#### `noImplicitAny`

"if you never want TypeScript to silently infer `any` for a type without you explicitly saying so, you can use `noImplicitAny` before you start modifying your files. While it might feel somewhat overwhelming, the long-term gains become apparent much more quickly." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"There are certain cases where TypeScript can’t figure out what certain types should be. To be as lenient as possible, it will decide to use the type `any` in its place. While this is great for migration, using `any` means that you’re not getting any type safety, and you won’t get the same tooling support you’d get elsewhere. You can tell TypeScript to flag these locations down and give an error with the `noImplicitAny` option." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"using `any` often defeats the purpose of using TypeScript in the first place. The more typed your program is, the more validation and tooling you’ll get, meaning you’ll run into fewer bugs as you code. Turning on the `noImplicitAny` flag will issue an error on any variables whose type is implicitly inferred as `any`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/basic-types.html))

#### `noImplicitThis`

"When you use the `this` keyword outside of classes, it has the type `any` by default." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

> imagine a `Point` class, and imagine a function that we wish to add as a method:
>
> ```ts
> class Point {
>   constructor(public x, public y) {}
>   getDistance(p: Point) {
>     let dx = p.x - this.x;
>     let dy = p.y - this.y;
>     return Math.sqrt(dx ** 2 + dy ** 2);
>   }
> }
> // ...
> // Reopen the interface.
> interface Point {
>   distanceFromOrigin(): number;
> }
> Point.prototype.distanceFromOrigin = function () {
>   return this.getDistance({ x: 0, y: 0 });
> };
> ```
>
> . . . we could easily have misspelled `getDistance` and not gotten an error.
>
> For this reason, TypeScript has the `noImplicitThis` option. When that option is set, TypeScript will issue an error when this is used without an explicit (or inferred) type.
>
> The fix is to use a `this`-parameter to give an explicit type in the interface or in the function itself:
>
> ```ts
> Point.prototype.distanceFromOrigin = function (this: Point) {
>   return this.getDistance({ x: 0, y: 0 });
> };
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

#### `strictNullChecks`

"By default, values like `null` and `undefined` are assignable to any other type. This can make writing some code easier, but forgetting to handle `null` and `undefined` is the cause of countless bugs . . . The `strictNullChecks` flag makes handling `null` and `undefined` more explicit, and spares us from worrying about whether we forgot to handle `null` and `undefined`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/basic-types.html))

"When `strictNullChecks` is enabled, `null` and `undefined` get their own types called `null` and `undefined` respectively. Whenever anything is possibly `null`, you can use a union type with the original type. So for instance, if something could be a `number` or `null`, you’d write the type out as `number | null`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"when using `strictNullChecks`, your dependencies may need to be updated to use `strictNullChecks` as well." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

# Compiler

## Configuration

> TypeScript uses a file called `tsconfig.json` for managing your project’s options, such as which files you want to include, and what sorts of checking you want to perform. Let’s create a bare-bones one for our project:
>
> ```json
> {
>   "compilerOptions": {
>     "outDir": "./built",
>     "allowJs": true,
>     "target": "es5"
>   },
>   "include": ["./src/**/*"]
> }
> ```
>
> Here we’re specifying a few things to TypeScript:
>
> 1.  Read in any files it understands in the `src` directory (with `include`).
> 2.  Accept JavaScript files as inputs (with `allowJs`).
> 3.  Emit all of the output files in `built` (with `outDir`).
> 4.  Translate newer JavaScript constructs down to an older version like ECMAScript 5 (using `target`).
>     At this point, if you try running `tsc` at the root of your project, you should see output files in the `built` directory. The layout of files in `built` should look identical to the layout of `src`. You should now have TypeScript working with your project.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

> You can also catch certain bugs with options like:
>
> - `noImplicitReturns` which prevents you from forgetting to return at the end of a function.
> - `noFallthroughCasesInSwitch` which is helpful if you never want to forget a break statement between cases in a switch block.
>   TypeScript will also warn about unreachable code and labels, which you can disable with `allowUnreachableCode` and `allowUnusedLabels` respectively.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

## Output

"although there were errors, the . . . file is still created. You can use TypeScript even if there are errors in your code. But in this case, TypeScript is warning that your code will likely not run as expected." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-tooling-in-5-minutes.html))

"If, for instance, you don’t want TypeScript to compile to JavaScript in the face of errors, you can use the `noEmitOnError` option." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))
