# TypeScript Reference

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

## Primitive Types

"There is already a small set of primitive types available in JavaScript: `boolean`, `bigint`, `null`, `number`, `string`, `symbol`, and `undefined`, which you can use in an interface. TypeScript extends this list with a few more, such as `any` (allow anything), `unknown` (ensure someone using this type declares what the type is), `never` (it’s not possible that this type could happen), and `void` (a function which returns `undefined` or has no return value)." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

## Type Definition

### Use Case

"some design patterns make it difficult for types to be inferred automatically (for example, patterns that use dynamic programming). To cover these cases, TypeScript supports an extension of the JavaScript language, which offers places for you to tell TypeScript what the types should be." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

### Interfaces

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

### Interfaces vs. Types

"there are two syntaxes for building types: Interfaces and Types. You should prefer `interface`. Use `type` when you need specific features." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

## Type Composition

### Overview

"you can create complex types by combining simple ones. There are two popular ways to do so: with unions, and with generics." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

### Unions

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

# Type Checking

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

## Structural Type System

"One of TypeScript’s core principles is that type checking focuses on the shape that values have. This is sometimes called “duck typing” or “structural typing”. In a structural type system, if two objects have the same shape, they are considered to be of the same type." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

"If the object or class has all the required properties, TypeScript will say they match, regardless of the implementation details." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

"In TypeScript, objects are _not_ of a single exact type. For example, if we construct an object that satisfies an interface, we can use that object where that interface is expected even though there was no declarative relationship between the two. . . . TypeScript’s type system is _structural_, not nominal" ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html))

"TypeScript’s type system is also not _reified_: There’s nothing at runtime that will tell us that `obj` is `Pointlike`. In fact, the `Pointlike` type is not present in any form at runtime." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html))

"In C# or Java, it’s meaningful to think of a one-to-one correspondence between runtime types and their compile-time declarations. In TypeScript, it’s better to think of a type as a set of values that share something in common. Because types are just sets, a particular value can belong to many sets at the same time. . . . we can think of `obj` as being a member of both the `Pointlike` set of values and the `Named` set of values." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-oop.html))
