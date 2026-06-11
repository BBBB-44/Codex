---
---

# TypeScript Interfaces

In TypeScript, an **interface** defines the *shape* of an object. It acts as a contract that specifies what properties and methods a value must have. Interfaces are used only during development for type checking and do **not generate JavaScript code at runtime**.

---

## Why Interfaces Are Useful

* Enforce structure in your code
* Catch mistakes early at compile time
* Improve readability and maintainability

---

## Key Features

### 1. Object Blueprint

Interfaces define property names and their types to ensure consistency across your codebase.

### 2. Optional Properties

Use `?` to make a property optional:

```ts
email?: string
```

### 3. Read-only Properties

Use `readonly` to prevent modification after assignment:

```ts
readonly joinDate: Date
```

### 4. Extensibility

Interfaces can inherit from one or more interfaces using `extends`.

### 5. Declaration Merging

If two interfaces share the same name, TypeScript automatically merges them into one.

---

## Basic Syntax

```ts
interface User {
  id: number;
  name: string;
  email?: string; // Optional
  readonly joinDate: Date; // Cannot be changed after creation
}

const newUser: User = {
  id: 1,
  name: "Jane Doe",
  joinDate: new Date()
};
```

---

## When to Use Interfaces vs Types

Although `interface` and `type` are similar, they have different strengths.

| Feature             | Interface                        | Type Alias                     |
| ------------------- | -------------------------------- | ------------------------------ |
| Object shapes       | Primary use case                 | Supported                      |
| Extending           | Uses `extends`                   | Uses `&` (intersection)        |
| Declaration merging | Yes                              | No                             |
| Union / tuple types | Not supported                    | Supported                      |
| Performance         | Generally faster in simple cases | Can be slower in complex cases |

---

### Recommendation

> Default to `interface` for object structures until you specifically need features only available in types (like unions or mapped types)

---

## Extending Types

It is common to build more specific types from existing ones.

### Example: Basic Address

we might have a BasicAddress type that describes the fields necessary for sending letters and packages in the U.S.

```ts
interface BasicAddress {
  name?: string;
  street: string;
  city: string;
  country: string;
  postalCode: string;
}
```

### Extended Version

In some situations that’s enough, but addresses often have a unit number associated with them if the building at an address has multiple units. We can then describe an AddressWithUnit.

```ts
interface AddressWithUnit {
  name?: string;
  unit: string;
  street: string;
  city: string;
  country: string;
  postalCode: string;
}
```

This does the job, but the downside here is that we had to repeat all the other fields from BasicAddress when our changes were purely additive. Instead, we can extend the original BasicAddress type and just add the new fields that are unique to AddressWithUnit.

---

### Better Approach: Extending an Interface

```ts
interface BasicAddress {
  name?: string;
  street: string;
  city: string;
  country: string;
  postalCode: string;
}

interface AddressWithUnit extends BasicAddress {
  unit: string;
}
```

### Why this is better

* Avoids duplication
* Makes relationships between types explicit
* Easier to maintain

---

## Multiple Inheritance

The extends keyword on an interface allows us to effectively copy members from other named types, and add whatever new members we want. This can be useful for cutting down the amount of type declaration boilerplate we have to write, and for signaling intent that several different declarations of the same property might be related. For example, AddressWithUnit didn’t need to repeat the street property, and because street originates from BasicAddress, a reader will know that those two types are related in some way.
interfaces can also extend from multiple types.

```ts
interface Colorful {
  color: string;
}

interface Circle {
  radius: number;
}

interface ColorfulCircle extends Colorful, Circle {}

const cc: ColorfulCircle = {
  color: "red",
  radius: 42
};
```
