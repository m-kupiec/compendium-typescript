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
    - `Symbol`
    - `never`
  - Complex Types
    - Arrays
    - Promises
    - Objects
- **Type Definition**
  - Overview
  - Type Annotation
  - Interfaces vs. Type Aliases
    - Differences
    - Choice
  - Interface Declaration
    - Objects
    - Classes
    - Functions
  - Type Alias
- **Type Composition**
  - Overview
  - Unions
    - General
    - Discriminated Unions
  - Generics
- **Describing Functions**
  - Function Type Expression
  - Call Signature
  - Construct Signature
  - Generic Function
    - Type Parameters
    - Constraints
    - Specifying Type Arguments
  - Optional & Default Parameters
- **Miscellaneous**
  - Type Assertion
  - Non-Null Assertion Operator
  - Type Literals
  - Type Predicate
  - Function Overload Signature
  - Modules
    - Importing Modules
    - Exporting from Modules
    - Using Libraries

### Type Checker

- **Overview**
- **Structural Type System**
- **Type Inference**
- **Type Narrowing**
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

> With `strictNullChecks` on, when a value is `null` or `undefined`, you will need to test for those values before using methods or properties on that value. Just like checking for `undefined` before using an optional property, we can use _narrowing_ to check for values that might be `null`:
>
> ```ts
> function doSomething(x: string | null) {
>   if (x === null) {
>     // do nothing
>   } else {
>     console.log("Hello, " + x.toUpperCase());
>   }
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

#### `Object`/`{}`/`any`

"You might be tempted to use `Object` or `{}` to say that a value can have any property on it . . . However `any` is actually the type you want to use in those situations, since it’s the most flexible type. For instance, if you have something that’s typed as `Object` you won’t be able to call methods like `toLowerCase()` on it. . . . `any` is special in that it is the most general type while still allowing you to do anything with it. That means you can call it, construct it, access properties on it, etc." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"whenever you use `any`, you lose out on most of the error checking and editor support that TypeScript gives you." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

"If a decision ever comes down to `Object` and `{}`, you should prefer `{}`. While they are mostly the same, technically `{}` is a more general type than `Object` in certain esoteric cases." ([TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html))

#### `Symbol`

> ```ts
> const firstName = Symbol("name");
> const secondName = Symbol("name");
>
> if (firstName === secondName) {
>   // Can't ever happen
> }
> ```
>
> ```ts
> This comparison appears to be unintentional because the types 'typeof firstName' and 'typeof secondName' have no overlap.
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

#### `never`

"When narrowing, you can reduce the options of a union to a point where you have removed all possibilities and have nothing left. In those cases, TypeScript will use a `never` type to represent a state which shouldn’t exist." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html))

> The `never` type is assignable to every type; however, no type is assignable to `never` (except `never` itself). This means you can use narrowing and rely on `never` turning up to do exhaustive checking in a `switch` statement.
>
> For example, adding a `default` to our `getArea` function which tries to assign the shape to `never` will not raise an error when every possible case has been handled.
>
> ```ts
> type Shape = Circle | Square;
>
> function getArea(shape: Shape) {
>   switch (shape.kind) {
>     case "circle":
>       return Math.PI * shape.radius ** 2;
>     case "square":
>       return shape.sideLength ** 2;
>     default:
>       const _exhaustiveCheck: never = shape;
>       return _exhaustiveCheck;
>   }
> }
> ```
>
> Adding a new member to the `Shape` union, will cause a TypeScript error:
>
> ```ts
> interface Triangle {
>   kind: "triangle";
>   sideLength: number;
> }
>
> type Shape = Circle | Square | Triangle;
>
> function getArea(shape: Shape) {
>   switch (shape.kind) {
>     case "circle":
>       return Math.PI * shape.radius ** 2;
>     case "square":
>       return shape.sideLength ** 2;
>     default:
>       const _exhaustiveCheck: never = shape;
>       return _exhaustiveCheck;
>   }
> }
> ```
>
> ```ts
> Type 'Triangle' is not assignable to type 'never'.
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

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

### Interfaces vs. Type Aliases

#### Differences

"there are two syntaxes for building types: Interfaces and Types." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

"Almost all features of an `interface` are available in `type`" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

"the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

Limitations of interfaces:

- "Interfaces may only be used to declare the shapes of objects, not rename primitives." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

Limitations of type aliases:

- "Type aliases may not participate in declaration merging, but interfaces can." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))
- "Using interfaces with extends can often be more performant for the compiler than type aliases with intersections" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

#### Choice

"You should prefer `interface`. Use `type` when you need specific features." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html))

"For the most part, you can choose based on personal preference, and TypeScript will tell you if it needs something to be the other kind of declaration. If you would like a heuristic, use `interface` until you need to use features from `type`." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

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

#### General

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

> you can combine . . . [literal types] with non-literal types:
>
> ```ts
> interface Options {
>   width: number;
> }
> function configure(x: Options | "auto") {
>   // ...
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

#### Discriminated Unions

"When every type in a union contains a common property with literal types, TypeScript considers that to be a _discriminated union_, and can narrow out the members of the union." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html))

> ```ts
> interface Shape {
>   kind: "circle" | "square";
>   radius?: number;
>   sideLength?: number;
> }
> ```
>
> . . . We need to communicate what we know to the type checker. . . .
>
> ```ts
> interface Circle {
>   kind: "circle";
>   radius: number;
> }
>
> interface Square {
>   kind: "square";
>   sideLength: number;
> }
>
> type Shape = Circle | Square;
> ```
>
> . . . Let’s see what happens here when we try to access the `radius` of a `Shape`.
>
> ```ts
> function getArea(shape: Shape) {
>   return Math.PI * shape.radius ** 2;
> }
> ```
>
> ```ts
> Property 'radius' does not exist on type 'Shape'.
> Property 'radius' does not exist on type 'Square'.
> ```
>
> . . . only the union encoding of `Shape` will cause an error regardless of how `strictNullChecks` is configured.
>
> ```ts
> function getArea(shape: Shape) {
>   if (shape.kind === "circle") {
>     return Math.PI * shape.radius ** 2;
>   }
> }
> ```
>
> That got rid of the error! . . . In this case, `kind` was that common property (which is what’s considered a _discriminant_ property of `Shape`). Checking whether the `kind` property was `"circle"` got rid of every type in `Shape` that didn’t have a `kind` property with the type `"circle"`. That narrowed shape down to the type `Circle`.
>
> The same checking works with `switch` statements as well.
>
> . . . The important thing here was the encoding of `Shape`. Communicating the right information to TypeScript - that `Circle` and `Square` were really two separate types with specific `kind` fields - was crucial. Doing that lets us write type-safe TypeScript code
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

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

## Describing Functions

### Function Type Expression

> syntactically similar to arrow functions:
>
> ```ts
> function greeter(fn: (a: string) => void) {
>   fn("Hello, World");
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

"if a parameter type isn’t specified, it’s implicitly `any`" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html))

"the parameter name is required. The function type `(string) => void` means “a function with a parameter named `string` of type `any`“!" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html))

> we can use a type alias to name a function type:
>
> ```ts
> type GreetFunction = (a: string) => void;
> function greeter(fn: GreetFunction) {
>   // ...
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

### Call Signature

> In JavaScript, functions can have properties in addition to being callable. However, the function type expression syntax doesn’t allow for declaring properties. If we want to describe something callable with properties, we can write a _call signature_ in an object type:
>
> ```ts
> type DescribableFunction = {
>   description: string;
>   (someArg: number): boolean;
> };
> function doSomething(fn: DescribableFunction) {
>   console.log(fn.description + " returned " + fn(6));
> }
>
> function myFunc(someArg: number) {
>   return someArg > 3;
> }
> myFunc.description = "default description";
>
> doSomething(myFunc);
> ```
>
> Note that the syntax is slightly different compared to a function type expression - use `:` between the parameter list and the return type rather than `=>`.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

### Construct Signature

> JavaScript functions can also be invoked with the `new` operator. TypeScript refers to these as constructors because they usually create a new object. You can write a construct signature by adding the `new` keyword in front of a call signature:
>
> ```ts
> type SomeConstructor = {
>   new (s: string): SomeObject;
> };
> function fn(ctor: SomeConstructor) {
>   return new ctor("hello");
> }
> ```
>
> Some objects, like JavaScript’s `Date` object, can be called with or without `new`. You can combine call and construct signatures in the same type arbitrarily:
>
> ```ts
> interface CallOrConstruct {
>   (n?: number): string;
>   new (s: string): Date;
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

### Generic Function

#### Type Parameters

"It’s common to write a function where the types of the input relate to the type of the output, or where the types of two inputs are related in some way." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html))

> In TypeScript, _generics_ are used when we want to describe a correspondence between two values. We do this by declaring a _type parameter_ in the function signature:
>
> ```ts
> function firstElement<Type>(arr: Type[]): Type | undefined {
>   return arr[0];
> }
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

> We can use multiple type parameters as well. For example, a standalone version of `map` would look like this:
>
> ```ts
> function map<Input, Output>(
>   arr: Input[],
>   func: (arg: Input) => Output
> ): Output[] {
>   return arr.map(func);
> }
>
> // Parameter 'n' is of type 'string'
> // 'parsed' is of type 'number[]'
> const parsed = map(["1", "2", "3"], (n) => parseInt(n));
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

> pair of similar functions:
>
> ```ts
> function filter1<Type>(arr: Type[], func: (arg: Type) => boolean): Type[] {
>   return arr.filter(func);
> }
>
> function filter2<Type, Func extends (arg: Type) => boolean>(
>   arr: Type[],
>   func: Func
> ): Type[] {
>   return arr.filter(func);
> }
> ```
>
> We’ve created a type parameter `Func` that _doesn’t relate two values_. That’s always a red flag, because it means callers wanting to specify type arguments have to manually specify an extra type argument for no reason. `Func` doesn’t do anything but make the function harder to read and reason about!
>
> **Rule**: Always use as few type parameters as possible
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

> Sometimes we forget that a function might not need to be generic:
>
> ```ts
> function greet<Str extends string>(s: Str) {
>   console.log("Hello, " + s);
> }
>
> greet("world");
> ```
>
> We could just as easily have written a simpler version:
>
> ```ts
> function greet(s: string) {
>   console.log("Hello, " + s);
> }
> ```
>
> Remember, type parameters are for _relating the types of multiple values_. If a type parameter is only used once in the function signature, it’s not relating anything. This includes the inferred return type; for example, if `Str` was part of the inferred return type of `greet`, it would be relating the argument and return types, so would be used _twice_ despite appearing only once in the written code.
>
> **Rule**: If a type parameter only appears in one location, strongly reconsider if you actually need it
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

#### Constraints

> Sometimes we want to relate two values, but can only operate on a certain subset of values. In this case, we can use a _constraint_ to limit the kinds of types that a type parameter can accept. We _constrain_ the type parameter to that type by writing an `extends` clause:
>
> ```ts
> function longest<Type extends { length: number }>(a: Type, b: Type) {
>   if (a.length >= b.length) {
>     return a;
>   } else {
>     return b;
>   }
> }
>
> // longerArray is of type 'number[]'
> const longerArray = longest([1, 2], [1, 2, 3]);
> // longerString is of type 'alice' | 'bob'
> const longerString = longest("alice", "bob");
> // Error! Numbers don't have a 'length' property
> const notOK = longest(10, 100);
> ```
>
> ```ts
> Argument of type 'number' is not assignable to parameter of type '{ length: >number; }'.
> ```
>
> . . . Because we constrained `Type` to `{ length: number }`, we were allowed to access the `.length` property of the `a` and `b` parameters. Without the type constraint, we wouldn’t be able to access those properties because the values might have been some other type without a `length` property.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

> Here’s a common error when working with generic constraints:
>
> ```ts
> function minimumLength<Type extends { length: number }>(
>   obj: Type,
>   minimum: number
> ): Type {
>   if (obj.length >= minimum) {
>     return obj;
>   } else {
>     return { length: minimum };
>   }
> }
> ```
>
> ```ts
> Type '{ length: number; }' is not assignable to type 'Type'.
>   '{ length: number; }' is assignable to the constraint of type 'Type', but 'Type' could be instantiated with a different subtype of constraint '{ length: number; }>'.
> ```
>
> It might look like this function is OK - `Type` is constrained to `{ length: number }`, and the function either returns `Type` or a value matching that constraint. The problem is that the function promises to return the _same_ kind of object as was passed in, not just _some_ object matching the constraint. If this code were legal, you could write code that definitely wouldn’t work:
>
> ```ts
> // 'arr' gets value { length: 6 }
> const arr = minimumLength([1, 2, 3], 6);
> // and crashes here because arrays have
> // a 'slice' method, but not the returned object!
> console.log(arr.slice(0));
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

> Here are two ways of writing a function that appear similar:
>
> ```ts
> function firstElement1<Type>(arr: Type[]) {
>   return arr[0];
> }
>
> function firstElement2<Type extends any[]>(arr: Type) {
>   return arr[0];
> }
>
> // a: number (good)
> const a = firstElement1([1, 2, 3]);
> // b: any (bad)
> const b = firstElement2([1, 2, 3]);
> ```
>
> These might seem identical at first glance, but `firstElement1` is a much better way to write this function. Its inferred return type is `Type`, but `firstElement2`’s inferred return type is `any` . . .
>
> **Rule**: When possible, use the type parameter itself rather than constraining it
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

#### Specifying Type Arguments

> TypeScript can usually infer the intended type arguments in a generic call, but not always. For example, let’s say you wrote a function to combine two arrays:
>
> ```ts
> function combine<Type>(arr1: Type[], arr2: Type[]): Type[] {
>   return arr1.concat(arr2);
> }
> ```
>
> Normally it would be an error to call this function with mismatched arrays:
>
> ```ts
> const arr = combine([1, 2, 3], ["hello"]);
> ```
>
> ```ts
> Type 'string' is not assignable to type 'number'.
> ```
>
> If you intended to do this, however, you could manually specify `Type`:
>
> ```ts
> const arr = combine<string | number>([1, 2, 3], ["hello"]);
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

### Optional & Default Parameters

> marking the parameter as optional with `?`:
>
> ```ts
> function f(x?: number) {
>   // ...
> }
> f(); // OK
> f(10); // OK
> ```
>
> Although the parameter is specified as type `number`, the `x` parameter will actually have the type `number | undefined` because unspecified parameters in JavaScript get the value `undefined`.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

> What people usually intend when writing `index?` as an optional parameter is that they want both of these calls to be legal:
>
> ```ts
> myForEach([1, 2, 3], (a) => console.log(a));
> myForEach([1, 2, 3], (a, i) => console.log(a, i));
> ```
>
> What this _actually_ means is that _callback might get invoked with one argument_.
>
> . . . TypeScript will enforce this meaning and issue errors that aren’t really possible:
>
> ```ts
> myForEach([1, 2, 3], (a, i) => {
>   console.log(i.toFixed());
> });
> ```
>
> ```ts
> 'i' is possibly 'undefined'.
> ```
>
> **Rule**: When writing a function type for a callback, _never_ write an optional parameter unless you intend to _call_ the function without passing that argument
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

> You can also provide a parameter default:
>
> ```ts
> function f(x = 10) {
>   // ...
> }
> ```
>
> Now in the body of `f`, `x` will have type `number` because any `undefined` argument will be replaced with `10`. Note that when a parameter is optional, callers can always pass `undefined`, as this simply simulates a “missing” argument
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html)

## Miscellaneous

### Type Assertion

> Sometimes you will have information about the type of a value that TypeScript can’t know about. For example, if you’re using `document.getElementById`, TypeScript only knows that this will return _some_ kind of `HTMLElement`, but you might know that your page will always have an `HTMLCanvasElement` with a given ID. In this situation, you can use a _type assertion_ to specify a more specific type:
>
> ```ts
> const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
> ```
>
> You can also use the angle-bracket syntax (except if the code is in a `.tsx` file), which is equivalent:
>
> ```ts
> const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

"TypeScript only allows type assertions which convert to a _more specific_ or _less specific_ version of a type. This rule prevents “impossible” coercions like: `const x = "hello" as number;`" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

"Sometimes . . . will disallow more complex coercions that might be valid. If this happens, you can use two assertions, first to `any` (or `unknown` . . .), then to the desired type: `const a = expr as any as T;`" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

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

### Non-Null Assertion Operator

"a special syntax for removing `null` and `undefined` from a type without doing any explicit checking. Writing `!` after any expression is effectively a type assertion that the value isn’t `null` or `undefined`" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

> If you ever have a value that TypeScript thinks is possibly `null`/`undefined`, but you know better, you can use the postfix `!` operator to tell it otherwise.
>
> ```ts
> declare var foo: string[] | null;
> foo.length; // error - 'foo' is possibly 'null'
> foo!.length; // okay - 'foo!' just has type 'string[]'
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html)

### Type Literals

> ```ts
> declare function handleRequest(url: string, method: "GET" | "POST"): void;
>
> const req = { url: "https://example.com", method: "GET" };
> handleRequest(req.url, req.method);
> ```
>
> ```ts
> Argument of type 'string' is not assignable to parameter of type '"GET" | "POST"'.
> ```
>
> In the above example `req.method` is inferred to be string, not `"GET"`.
>
> There are two ways to work around this.
>
> 1.  You can change the inference by adding a type assertion in either location:
>
>     ```ts
>     // Change 1:
>     const req = { url: "https://example.com", method: "GET" as "GET" };
>     // Change 2
>     handleRequest(req.url, req.method as "GET");
>     ```
>
>     Change 1 means “I intend for req.method to always have the _literal_ type `"GET"`”, preventing the possible assignment of `"GUESS"` to that field after. Change 2 means >“I know for other reasons that `req.method` has the value `"GET"`“.
>
> 2.  You can use `as const` to convert the entire object to be type literals:
>
>     ```ts
>     const req = { url: "https://example.com", method: "GET" } as const;
>     handleRequest(req.url, req.method);
>     ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

### Type Predicate

"To define a user-defined type guard, we simply need to define a function whose return type is a _type predicate_" ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html))

"_Type Predicate Functions_ are functions that return a `boolean` value and have a particular return type syntax. A _type predicate_ is a type assertion that checks if an object has a specific property or set of properties. This allows TypeScript to narrow (or refine) the type of an object based on the result of the function." ([Matias Hernández](https://matiashernandez.dev/blog/post/what-are-type-predicates-in-typescript))

Pros:

> One of the major advantages of type predicate functions is that they provide a way to express complex type relationships in a readable and understandable way. They allow you to define custom functions that not only perform a specific task but also return a boolean value that tells TypeScript whether a variable is of a particular type. This can make your code more expressive and self-documenting.
>
> They can also be useful when you need to perform dynamic type checks on an object. For example, imagine you have a function that takes an object as an argument, but you’re not sure whether the object has a specific property. With a type predicate function, you can check for the presence of that property and narrow the type of the object to include that property.
>
> [Matias Hernández](https://matiashernandez.dev/blog/post/>>what-are-type-predicates-in-typescript)

Cons:

> the most important problem of this functions is a risk, there is an easy way to introduce bugs to the process. You can wirte incorrect predicates leading to unexpected or undesired type narrowing. This can result in runtime errors or unexpected behavior, which can be difficult to diagnose and fix.
>
> Type predicates ressembles the use (and pitfalls) of using `as` for type assertions, you can lie to the type system, it equals to say “I know more about this type than the compiler” and force the type to be the desired one, as an example:
>
> ```ts
> function isString(x: unknown): x is string {
>   return typeof x === "number";
> }
> ```
>
> The above example check if `x` is a `number`, and if that is `true` then the predicate say that the variable is a `string`. If later you use that type predicate, TS assume that the variable is an `string` and the type safety will be lost.
>
> [Matias Hernández](https://matiashernandez.dev/blog/post/>what-are-type-predicates-in-typescript)

> ```ts
> function isFish(pet: Fish | Bird): pet is Fish {
>   return (pet as Fish).swim !== undefined;
> }
> ```
>
> `pet is Fish` is our type predicate in this example. A predicate takes the form `parameterName is Type`, where `parameterName` must be the name of a parameter from the current function signature. Any time `isFish` is called with some variable, TypeScript will narrow that variable to that specific type if the original type is compatible.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

> ```ts
> // Both calls to 'swim' and 'fly' are now okay.
> let pet = getSmallPet();
>
> if (isFish(pet)) {
>   pet.swim();
> } else {
>   pet.fly();
> }
> ```
>
> Notice that TypeScript not only knows that `pet` is a `Fish` in the `if` branch; it also knows that in the `else` branch, you don’t have a `Fish`, so you must have a `Bird`.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

> You may use the type guard `isFish` to filter an array of `Fish | Bird` and obtain an array of `Fish`:
>
> ```ts
> const zoo: (Fish | Bird)[] = [getSmallPet(), getSmallPet(), getSmallPet()];
> const underWater1: Fish[] = zoo.filter(isFish);
> // or, equivalently
> const underWater2: Fish[] = zoo.filter(isFish) as Fish[];
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

> ```ts
> // The predicate may need repeating for more complex examples
> const underWater3: Fish[] = zoo.filter((pet): pet is Fish => {
>   if (pet.name === "sharkey") return false;
>   return isFish(pet);
> });
> ```
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

"classes can use `this is Type` to narrow their type." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html))

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

> ```js
> let x = Math.random() < 0.5 ? 10 : "hello world!";
>
> /* . . . */
> ```
>
> - ```ts
>   let x: string | number;
>   ```
>
> ```js
> /* . . . */
>
> x = 1;
>
> /* . . . */
> ```
>
> - ```ts
>   let x: number;
>   ```
>
> ```js
> /* . . . */
>
> x = "goodbye!";
> ```
>
> - ```ts
>   let x: string;
>   ```
>
> Notice that each of these assignments is valid. Even though the observed type of `x` changed to `number` after our first assignment, we were still able to assign a `string` to `x`. This is because the declared type of `x` - the type that `x` started with - is `string | number`, and assignability is always checked against the declared type. If we’d assigned a `boolean` to `x`, we’d have seen an error since that wasn’t part of the declared type.
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

"Point-free programming — heavy use of currying and function composition — is possible in JavaScript, but can be verbose. In TypeScript, type inference often fails for point-free programs, so you’ll end up specifying type parameters instead of value parameters. The result is so verbose that it’s usually better to avoid point-free programming." ([TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html))

## Type Narrowing

"Narrowing occurs when TypeScript can deduce a more specific type for a value based on the structure of the code." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html))

"TypeScript sees `typeof padding === "number"` and understands that as a special form of code called a _type guard_. TypeScript follows possible paths of execution that our programs can take to analyze the most specific possible type of a value at a given position. It looks at these special checks (called _type guards_) and assignments, and the process of refining types to more specific types than declared is called _narrowing_." ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html))

> There are a couple of different constructs TypeScript understands for narrowing.
>
> - `typeof` type guards . . .
> - Truthiness narrowing . . .
>   - Equality narrowing . . .
>   - The `in` operator narrowing . . .
>   - `instanceof` narrowing . . .
>   - Assignments . . .
>   - Control flow analysis . . .
>   - Type predicates . . .
>   - Assertion functions . . .
> - Discriminated unions . . .
> - The `never` type . . .
> - Exhaustiveness checking
>
> [TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

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

> ```ts
> interface Shape {
>   kind: "circle" | "square";
>   radius?: number;
>   sideLength?: number;
> }
> ```
>
> . . . outside of `strictNullChecks` we’re able to accidentally access any of those fields anyway (since optional properties are just assumed to always be present when reading them).

[TypeScript](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

> with this TypeScript code, `users.find` has no guarantee that it will actually find a user, but you can write code as though it will:
>
> ```ts
> declare const loggedInUsername: string;
>
> const users = [
>   { name: "Oby", age: 12 },
>   { name: "Heera", age: 32 },
> ];
>
> const loggedInUser = users.find((u) => u.name === loggedInUsername);
> console.log(loggedInUser.age);
> ```
>
> Setting `strictNullChecks` to `true` will raise an error that you have not made a >guarantee that the `loggedInUser` exists before trying to use it.
>
> ```ts
> 'loggedInUser' is possibly 'undefined'.
> ```
>
> [TypeScript](https://www.typescriptlang.org/tsconfig/#strictNullChecks)

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
