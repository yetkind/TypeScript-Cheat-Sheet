# TypeScript Cheat Sheet
Extended and detailed TypeScript cheat sheet.

Index

1. [Introduction](#introduction)
2. [Basic Types](#basic-types)
3. [Type Inference](#type-inference)
4. [Functions](#functions)
5. [Interfaces](#interfaces)
6. [Classes](#classes)
7. [Enums](#enums)
8. [Generics](#generics)
9. [Utility Types](#utility-types)
10. [Modules](#modules)
11. [Type Guards](#type-guards)
12. [Decorators](#decorators)

---

## Introduction

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It provides static typing, interfaces, and other features to improve the development experience and catch potential bugs during compile time. This cheat sheet assumes you already know JavaScript 

---

## Basic Types

- **Boolean**: `let isDone: boolean = false;`
  
- **Number**: `let decimal: number = 10;`
  
- **String**: `let name: string = 'TypeScript';`
  
- **Array**:
  
  ```ts
  let list: number[] = [1, 2, 3];
  let genericList: Array<number> = [1, 2, 3];
  ```
  
- **Tuple**: `let tuple: [string, number] = ['TypeScript', 10];`
  
- **Enum**:
  
  ```ts
  enum Direction { Up, Down, Left, Right }
  let dir: Direction = Direction.Up;
  ```
  
- **Any**: `let notSure: any = 4;`
  
- **Void**: Used for functions that return no value.
  
  ```ts
  function warnUser(): void {
      console.log("This is a warning message");
  }
  ```
  
- **Null and Undefined**: `let u: undefined = undefined;`
  
- **Never**: Represents the type of values that never occur.
  
  ```ts
  function error(message: string): never {
    throw new Error(message);
  }
  ```
  

---

## Type Inference

TypeScript will infer the type if it is not explicitly specified.

```ts
let inferredString = 'Hello'; // TypeScript infers this as string.
let inferredNumber = 13;      // TypeScript infers this as number.
```

---

## Functions

### Basic Function

```ts
function add(x: number, y: number): number {
  return x + y;
}
```

### Optional Parameters and Default Values

```ts
function buildName(firstName: string, lastName?: string): string {
  return lastName ? `${firstName} ${lastName}` : firstName;
}

function buildNameWithDefault(firstName: string, lastName = "Yetkin"): string {
  return `${firstName} ${lastName}`;
}
```

### Rest Parameters

```ts
function sum(...numbers: number[]): number {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}
```

---

## Interfaces

Interfaces define the shape of objects and can enforce certain properties.

```ts
interface User {
  name: string;
  age: number;
  isAdmin?: boolean; // Optional property
}

function greet(user: User) {
  return `Hello, ${user.name}`;
}
```

### Extending Interfaces

```ts
interface Admin extends User {
  permissions: string[];
}
```

---

## Classes

### Basic Class

```ts
class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }

  greet() {
    return `Hello, ${this.name}`;
  }
}
```

### Inheritance

```ts
class Employee extends Person {
  position: string;
  constructor(name: string, position: string) {
    super(name);
    this.position = position;
  }

  work() {
    return `${this.name} is working as a ${this.position}`;
  }
}
```

### Public, Private, and Protected Modifiers

- `public`: Default, accessible everywhere.
- `private`: Only accessible within the class.
- `protected`: Accessible within the class and subclasses.

```ts
class EncapsulatedPerson {
  protected name: string;
  private ssn: string;

  constructor(name: string, ssn: string) {
    this.name = name;
    this.ssn = ssn;
  }

  getName(): string {
    return this.name;
  }
}
```

---

## Enums

Enums allow for defining a set of named constants.

```ts
enum Color { Red = 1, Green, Blue }
let colorName: string = Color[2]; // 'Green'
```

---

## Generics

Generics allow for creating reusable components.

```ts
function identity<T>(arg: T): T {
  return arg;
}

let output = identity<string>("TypeScript"); // Explicit type
let inferredOutput = identity(13); // Inferred type
```

### Generic Constraints

```ts
function loggingIdentity<T extends { length: number }>(arg: T): T {
  console.log(arg.length); // `length` is a property.
  return arg;
}
```

---

## Utility Types

### Partial

```ts
interface Todo {
  title: string;
  description: string;
}

let todo: Partial<Todo> = {
  title: "Write cheatsheet"
};
```

### Readonly

```ts
interface Todo {
  title: string;
}

let todo: Readonly<Todo> = {
  title: "Write cheatsheet"
};

// todo.title = "New Title"; // Error: Cannot assign to 'title' because it is a read-only property.
```

### Record

```ts
let nameAgeMap: Record<string, number> = {
  Yetkin: 25,
  Miller: 30
};
```

---

## Modules

### Exporting and Importing

```ts
// math.ts
export function add(x: number, y: number): number {
  return x + y;
}

// app.ts
import { add } from './math';
console.log(add(1, 2)); // 3
```

### Default Exports

```ts
// defaultMath.ts
export default function subtract(x: number, y: number): number {
  return x - y;
}

// app.ts
import subtract from './defaultMath';
console.log(subtract(5, 3)); // 2
```

---

## Type Guards

Type guards help with narrowing down types.

```ts
function isString(x: any): x is string {
  return typeof x === 'string';
}

function print(x: string | number) {
  if (isString(x)) {
    console.log(x.toUpperCase());
  } else {
    console.log(x.toFixed(2));
  }
}
```

---

## Decorators

Decorators are used to modify classes and methods.

```ts
function Log(target: any, key: string, descriptor: PropertyDescriptor) {
  const original = descriptor.value;

  descriptor.value = function(...args: any[]) {
    console.log(`Calling ${key} with args: ${args}`);
    return original.apply(this, args);
  };

  return descriptor;
}

class Calculator {
  @Log
  add(a: number, b: number) {
    return a + b;
  }
}
```

---
Feel free to customize and extend this cheat sheet as you explore more advanced development topics!
