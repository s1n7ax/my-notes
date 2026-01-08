# Union vs Intersection

## Union vs Intersection | Primitives

### Union

```typescript
type A = string | number;
```

This declares that type A can be either a string or a number.

```typescript
type A = string | number;

// ✅ Valid assignments
let value1: A = "hello"; // string is allowed
let value2: A = 42; // number is allowed

// ❌ Invalid assignments
let value3: A = true; // Error: boolean is not assignable
let value4: A = null; // Error: null is not assignable
```

### Intersection

```typescript
type A = string & number;
```

In TypeScript, an intersection type using & means a value must satisfy all types simultaneously. The & symbol means "and".

```typescript
type A = string & number;

// ❌ No value can be assigned to this type
let value: A = "hello";  // Error
let value2: A = 42;      // Error
let value3: A = ...      // Nothing works!
```

## Union vs Intersection | Objects

### Union

With object types, unions are more complex because TypeScript uses structural typing and looks at the shape of objects

```typescript
type Cat = { name: string; meow: () => void };
type Dog = { name: string; bark: () => void };

let pet: Cat | Dog;

// You can only access properties that exist on BOTH types
console.log(pet.name); // ✓ valid - both have 'name'
pet.meow(); // ✗ error - might be a Dog
pet.bark(); // ✗ error - might be a Cat
```

#### Discriminated Unions

The most powerful pattern for object unions is using a discriminant property - a literal type that distinguishes between union members:

```typescript
type Cat = { type: "cat"; name: string; meow: () => void };
type Dog = { type: "dog"; name: string; bark: () => void };

type Pet = Cat | Dog;

function handlePet(pet: Pet) {
  // Type narrowing based on the discriminant
  if (pet.type === "cat") {
    pet.meow(); // ✓ TypeScript knows it's a Cat
  } else {
    pet.bark(); // ✓ TypeScript knows it's a Dog
  }
}
```

### Intersection

With object types, intersections merge properties from all types

```typescript
type Person = { name: string };
type Employee = { employeeId: number };

type Worker = Person & Employee;

const worker: Worker = {
  name: "Alice",
  employeeId: 123,
}; // ✅ Must have BOTH properties
```
