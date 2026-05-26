# Chapter 05: Generics

## 📚 Overview
Generics allow you to write reusable code that works with multiple types while maintaining type safety.

---

## 🎯 Key Concepts

### 1. Generic Functions

//typescript
// Without generics - loses type info
function identity(value: any): any {
  return value;
}

// With generics - preserves type
function identity<T>(value: T): T {
  return value;
}

// Usage
const num = identity<number>(42);      // Type: number
const str = identity("hello"); // Type: string
const inferred = identity(true);       // Type: boolean (inferred)
//

### 2. Generic Interfaces

//typescript
interface Container<T> {
  value: T;
  getValue(): T;
  setValue(value: T): void;
}

const numberContainer: Container<number> = {
  value: 42,
  getValue() { return this.value; },
  setValue(v) { this.value = v; }
};

// Generic interface with multiple types
interface Pair<K, V> {
  key: K;
  value: V;
}

const pair: Pair<string, number> = { key: "age", value: 30 };
//

### 3. Generic Classes

//typescript
class Stack<T> {
  private items: T[] = [];
  
  push(item: T): void {
    this.items.push(item);
  }
  
  pop(): T | undefined {
    return this.items.pop();
  }
  
  peek(): T | undefined {
    return this.items[this.items.length - 1];
  }
  
  isEmpty(): boolean {
    return this.items.length === 0;
  }
}

const numberStack = new Stack<number>();
numberStack.push(1);
numberStack.push(2);
numberStack.pop();  // 2

const stringStack = new Stack<string>();
stringStack.push("hello");
//

### 4. Generic Constraints

//typescript
// Constraint with extends
interface HasLength {
  length: number;
}

function logLength<T extends HasLength>(value: T): number {
  console.log(value.length);
  return value.length;
}

logLength("hello");     // OK - string has length
logLength([1, 2, 3]);   // OK - array has length
// logLength(42);       // Error - number has no length

// Constraint with keyof
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "John", age: 30 };
getProperty(user, "name");  // OK
// getProperty(user, "email");  // Error - "email" not in user
//

### 5. Multiple Type Parameters

//typescript
function map<T, U>(array: T[], fn: (item: T) => U): U[] {
  return array.map(fn);
}

const numbers = [1, 2, 3];
const strings = map(numbers, n => n.toString());
// Type: string[]

// Swap function
function swap<T, U>(tuple: [T, U]): [U, T] {
  return [tuple[1], tuple[0]];
} 

const swapped = swap(["hello", 42]);  // [42, "hello"]
//

### 6. Default Type Parameters

//typescript
interface ApiResponse<T = any> {
  data: T;
  status: number;
}

interface User {
  name: string;
}

const user: User = {
  name: "John"
};

const response1: ApiResponse = {
  data: "anything",
  status: 200
};

const response2: ApiResponse<User> = {
  data: user,
  status: 200
};
///
// Function with default
function createArray<T = string>(length: number, value: T): T[] {
  return Array(length).fill(value);
}

createArray(3, "x");  // string[]
createArray<number>(3, 0);  // number[]
//

### 7. Generic Utility Types

//typescript
// Partial - all properties optional
interface User {
  name: string;
  age: number;
}

type PartialUser = Partial<User>;
// { name?: string; age?: number; }

// Required - all properties required
type RequiredUser = Required<PartialUser>;

// Readonly - all properties readonly
type ReadonlyUser = Readonly<User>;

// Pick - select properties
type NameOnly = Pick<User, "name">;

// Omit - exclude properties
type WithoutAge = Omit<User, "age">;

// Record - create object type
type UserMap = Record<string, User>;
//
const users: UserMap = {
  emp101: { name: "John", age: 25 },
};

### 8. Conditional Types

//typescript
// Basic conditional type
type IsString<T> = T extends string ? true : false;

type A = IsString<string>;  // true
type B = IsString<number>;  // false
 
 const a1: A = true;
 const b1: B = false;




// Extract and Exclude
## keeps only the types from T that are also present in U
type T1 = Extract<"a" | "b" | "c", "a" | "f">;  // "a"
## removes types from T that are assignable to U
type T2 = Exclude<"a" | "b" | "c", "a">;        // "b" | "c"
const a: T1 = "a";
const b: T2 = "b";


// NonNullable
## removes null and undefined from T
type T3 = NonNullable<string | null | undefined>;  // string
const a3: T3 = "hello";
---
interface ApiResponse {
  username: string | null;
}

type SafeUsername = NonNullable<ApiResponse["username"]>;
const user1: SafeUsername = "Vinoth"; 
function printUsername(username: SafeUsername) {
  console.log(username.toUpperCase());
}

printUsername(user1);
---
// ReturnType
function getData() { return { id: 1, name: "John" }; }
type DataType = ReturnType<typeof getData>;
// { id: number; name: string; }
//

### 9. Mapped Types

//typescript
// Create readonly version
<!-- type Readonly<T> = {
  readonly [P in keyof T]: T[P];
}; -->

const r = { a: 1, b: 2 };
const ro: Readonly<typeof r> = { a: 1, b: 2 };


// Create optional version
type Optional<T> = {
  [P in keyof T]?: T[P];
};

const o = { a: 1, b: 2 };
const oo: Optional<typeof o> = { a: 1, b: 2 };


// Create nullable version
type Nullable<T> = {
  [P in keyof T]: T[P] | null;
};

const n = { a: 1, b: 2 };
const no: Nullable<typeof n> = { a: 1, b: 2 };
//

// Practical example
interface User {
  name: string;
  age: number;
}

type ReadonlyUser = Readonly<User>;
const readonlyUser: ReadonlyUser = { name: "John", age: 30 };
// readonlyUser.name = "Jane";
type OptionalUser = Optional<User>;
const optionalUser: OptionalUser = { name: "Jane" };

//

//

## 💻 Practice Exercises

1. Create generic functions
2. Build generic data structures
3. Use constraints effectively
4. Apply utility types
5. Create custom mapped types

---

## ✅ Best Practices

- ✅ Use meaningful type parameter names (T, K, V)
- ✅ Use constraints to limit types
- ✅ Use built-in utility types
- ✅ Provide default types when sensible
- ❌ Don't overuse generics
- ❌ Avoid overly complex type logic

---

## 📝 Quick Reference

//typescript
// Generic function
function fn<T>(arg: T): T { }


// Generic interface
interface Box<T> { value: T; }

// Generic class
class Container<T> { }

// Constraint
function fn<T extends HasLength>(arg: T) { }

// Utility types
Partial<T>  Required<T>  Readonly<T>
Pick<T, K>  Omit<T, K>   Record<K, V>
//

