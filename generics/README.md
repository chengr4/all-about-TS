# Generics

- We need a way of capturing the type of the argument in such a way that we can also use it to denote what is being returned.

> NOte: It is not possible to create generic enums and namespaces.

## Goal

- To create reusable components

---

## Generic Types

```typescript
function identity<Type>(arg: Type): Type {
  return arg;
}
 
let myIdentity: <Type>(arg: Type) => Type = identity;
```

compiles to JS:

```javascript
"use strict";
function identity(arg) {
    return arg;
}
let myIdentity = identity;
```

Object literal type + Interface (naming)

```typescript
interface GenericIdentityFn {
  <Type>(arg: Type): Type;
}
 
function identity<Type>(arg: Type): Type {
  return arg;
}
 
let myIdentity: GenericIdentityFn = identity;
```

## Generic Classes

> Generic classes are only generic over their instance side rather than their static side, so when working with classes, static members can not use the class’s type parameter.
 
## Generic Constraints

```typescript
// Create an interface that describes our constraint.
// Only types that also have the .length property can be the argument
interface Lengthwise {
  length: number;
}
 
function loggingIdentity<Type extends Lengthwise>(arg: Type): Type {
  console.log(arg.length); // Now we know it has a .length property, so no more error
  return arg;
}

loggingIdentity(3); // Error: Argument of type 'number' is not assignable to parameter of type 'Lengthwise'.
```

## Other Examples

```typescript
const last = <T>(arr: T[]) => {
  return arr[arr.length - 1];
}

const l2 = last<string>(["a", "b", "c"]);

const makeFullName = <T extends { firstName: string; lastName: string }>(
  obj: T
) => {
  return {
    ...obj,
    fullName: obj.first.Name + ' ' + obj.lastName
  };
}
```

With `interface`

```typescript
interface Tab<T> {
  id: string;
  position: number;
  data: T;
}

type numberTab = Tab<number>;

```

In React

```typescript
import React from "react";

interface Props {
  name: string
}

const HelloWorld: React.FC<Props> = ({ name }) => 

  return <div> hello {name}</div>;
}
```
