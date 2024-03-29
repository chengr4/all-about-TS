# All about TypeScript

- [Exclamation mark](#exclamation-mark)
- [interface](#interface)
- [type](#type)
- [Generics](./generics)
- [Enums](./enums/)
- [React](./react)
- [Finish Topics](#finished-topics)
- [Utility Types](./utility-types/)


## Exclamation mark `!`

That's the `non-null` assertion operator. It is a way to tell the compiler "this expression cannot be `null` or `undefined` here, so don't complain about the possibility of it being `null` or `undefined`." Sometimes the type checker is unable to make that determination itself. [^em-1]

## Index Signature

An index signature is defined using the `[key: type]` syntax, where `key` is the name of the property, and `type` is the type of the value that should be stored at that property

```typescript
// eg
interface MyObject {
  [key: string]: string;
}
```

## `interface`

> Interfaces are basically a way to describe data shapes, for example, an object

- TS only
- Enfore a certain structure of a class or object (define the shape) => Interfaces are better when you need to define a new object or method of an object.
- `interface` can extend another `interface`, `class`
- `interface` will merge same `interface` automatically (delcaration merging)
- `interface` does not have Union `|` feature

E.g.

In Function:

```typescript
interface RectangleOptions {
  width: number;
  length: number;
  height?: number; // with '?' tells TS height is optional
}

function drawRectangle(options: RectangleOptions) {
  let width = options.width;
  let length = options.length;
      
  // Draw logic
}

drawRectangle({
  width: 100,
  length: 50,
});
```

In Class:

```typescript

// with class
interface HasFormatter {
  format(): string;
}

interface IsPerson {
  name: string;
  age: number;
  speak(a: string): void;
  spend(a: number): number;
}

class Invoice implements HasFormatter {
  format() {
    return "XXXX"
  }
}

let invoice = new Invoice();
```

### `interface` extends `interface`

```typescript
interface Person {
  name: string;
  hungry: boolean;
}

interface Harry extends Person {
  youtuber: boolean;
}
```

## `type`

Type Alias

> Type is a definition of a type of data, for example, a union, primitive, intersection, tuple, or any other type.

- `type` cannot extend another `type`
- `type` has Union `|`, Intersection `&` features
- Functions are better `type` than `interface`

```typescript
type Hungry = boolean;
type Greeting = (name: string) => string;

type Person = {
  name: string;
}

type Youtuber = {
  youtuber: boolean;
}

// Use Union
type Harry = Person | Youtuber;
```

### Tuple

A tuple type is another sort of Array type that knows exactly how many elements it contains, and exactly which types it contains at specific positions.

> we can only declare tuples using types and not interfaces.

```typescript
type Reponse = [string, number]
```

## Finished Topics

- [x] [Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)

- [ ] [Enums](https://www.typescriptlang.org/docs/handbook/enums.html)
- [ ] [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)

## References

1. [The Net Ninja; TypeScript Tutorial #15 - Interfaces (2020.5)](https://youtu.be/VbW6vWTaHOY)
2. [Harry Wolff; TypeScript Interfaces vs Types (2020.5)](https://youtu.be/crjIq7LEAYw)
3. [Ben Awad; Typescript Generics Tutorial (2019.8)](https://youtu.be/nViEqpgwxHE)
4. [Leonardo Maldonado; Types vs. interfaces in TypeScript (2020.5)](https://blog.logrocket.com/types-vs-interfaces-in-typescript/)

[^em-1]: https://stackoverflow.com/questions/42273853/in-typescript-what-is-the-exclamation-mark-bang-operator-when-dereferenci
