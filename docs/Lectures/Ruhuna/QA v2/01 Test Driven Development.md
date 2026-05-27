# Test Driven Development

by Srinesh Nisala (Senior Software Engineer @ iLabs)

- LinkedIn: [https://www.linkedin.com/in/srinesh-nisala/](https://www.linkedin.com/in/srinesh-nisala/)
- GitHub: [https://github.com/s1n7ax](https://github.com/s1n7ax)

---

## Pre-requisites

- Create a Github account
- Get a fork of [https://github.com/s1n7ax/lecture-tdd-v2](https://github.com/s1n7ax/lecture-tdd-v2)
- Open the project with Codespace

---

## Project structure

- Explain how to run tests

```shell
npm test
```

---

## Basics of Vitest

- Show what a test file looks like — `describe()`, `it()` and `expect()`
- Write a simple passing test to confirm the setup works

---

## Write all tests first

- Create `password.js` and `password.test.js`
- Write a test: short password returns `{ valid: false }`
- Write a test: 8-char password returns `{ valid: true }`
- Write a test: password with no uppercase returns `{ valid: false }`
- Write a test: password with no digit returns `{ valid: false }`
- Write a test: password with no special character returns `{ valid: false }`
- Run all tests — show all RED

---

## Exercise 1 — Minimum length

- Implement minimum code: check `password.length >= 8`
- Run tests — first two GREEN, rest still RED

---

## Exercise 2 — Uppercase

- Add the uppercase check (`/[A-Z]/`)
- Run tests — show GREEN

---

## Exercise 3 — Digit

- Add the digit check (`/[0-9]/`)
- Run tests — show GREEN

---

## Exercise 4 — Special character

- Add the special character check (`/[^a-zA-Z0-9]/`)
- Run tests — all GREEN
- Point out the smell: `{ valid: false, message }` repeated four times

---

## What is TDD?

> Test-Driven Development (TDD) is a Software development method in which you write Automation Tests before the actual development process starts

![](../../../../assets/red-green-refactor.png)

Red-Green-Refactor:

- Focus on testing behaviors (requirements) rather than implementation details.
- Write minimal code to pass tests ("green"),
- Refactor without adding new tests.

---

## Pros and Cons of TDD

**Pros**

- Tests act as living documentation — they show exactly what the code is supposed to do
- Gives confidence to refactor without breaking existing behaviour
- Forces you to think about the interface before the implementation

**Cons**

- Hard to apply to UI, databases, and external APIs without extra tooling
- Can give false confidence if tests only cover happy paths

---

## TDD Best Practices

- Reduce mocking and stubbing
- Avoid testing private/internal code; focus on public interfaces
- Avoid Over-Testing

---

## More on TDD

- [TDD, Where Did It All Go Wrong](https://www.youtube.com/watch?v=EZ05e7EMOLM)
- [Jim Coplien and Bob Martin Debate TDD](https://www.youtube.com/watch?v=KtHQGs3zFAM)
