
## Generic Types and Functions

[Generic Classes and Interfaces](#generic-classes-and-interfaces)  
[Generic Constraints](#generic-constraints)  
[Generic Functions](#generic-functions)  
[Generic Defaults](#generic-defaults)  

Generic types and functions allow creating the code capable to work over a variety of types rather than a single type.

### Generic Classes and Interfaces

A class and an interface can be defined as generics, adding parameters to the type definition, like the type parameter `Element` in the following example:

```typescript
class CustomStack<Element> {
  public push(e: Element):void {
    // ...
  }
}
```

To use type CustomStack, the type argument must be specified for each type parameter:

```typescript
let s = new CustomStack<string>();
s.push('hello');
```

Compiler ensures type safety while working with generic types and functions.
See below:

```typescript
let s = new CustomStack<string>();
s.push(55); // That will be a compile-time error as 55 is not compatible with type string.
```

### Generic Constraints

Type parameters of generic types can be bounded. For example, the `Key` type parameter in the `MyHashMap<Key, Value>` container must have the `hash` method.

```typescript
interface Hashable {
  hash(): number;
}
class MyHashMap<Key extends Hashable, Value> {
  public set(k: Key, v: Value) {
    let h = k.hash();
    // ... other code ...
  }
}
```

In the above example, the `Key` type extends `Hashable`, and all methods of `Hashable` interface can be called for keys.

### Generic Functions

Use a generic function to create a more universal code. Consider a function that returns the last element of the array:

```typescript
function last(x: number[]): number {
  return x[x.length - 1];
}
last([1, 2, 3]); // output: 3
```

If the same function needs to be defined for any array, then define it as a generic with a type parameter:

```typescript
function last<T>(x: T[]): T {
  return x[x.length - 1];
}
```

Now, the function can be used with any array.

In a function call, type argument can be set explicitly or implicitly:

```typescript
// Explicit type argument
last<string>(['aa', 'bb']);
last<number>([1, 2, 3]);

// Implicit type argument:
// Compiler understands the type argument based on the type of the call arguments
last([1, 2, 3]);
```

### Generic Defaults

Type parameters of generic types can have defaults. It allows using just the generic type name instead of specifying the actual type arguments.
The example below illustrates this for both classes and functions.

```typescript
class SomeType {}
interface Interface <T1 = SomeType> { }
class Base <T2 = SomeType> { }
class Derived1 extends Base implements Interface { }
// Derived1 is semantically equivalent to Derived2
class Derived2 extends Base<SomeType> implements Interface<SomeType> { }

function foo<T = number>(): T {
  // ...
}
foo();
// such function is semantically equivalent to the call below
foo<number>();
```
