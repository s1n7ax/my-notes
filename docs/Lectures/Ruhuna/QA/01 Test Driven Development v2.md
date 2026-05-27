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

- Show what a test file looks like — `it()` and `expect()`
- Write a simple passing test to confirm the setup works
- Introduce `beforeEach` and `afterEach`

---

## Exercise 1

- Create `password.js` and `password.test.js`
- Write a test: short password returns `{ valid: false }`
- Write a test: 8-char password returns `{ valid: true }`
- Run tests — show RED
- Implement minimum code: check `password.length >= 8`
- Run tests — show GREEN

---

## Exercise 2

- Write a test: password with no uppercase returns `{ valid: false }`
- Run tests — show RED
- Add the uppercase check
- Run tests — show GREEN

---

## Exercise 3

- Write a test: password with no digit returns `{ valid: false }`
- Run tests — show RED
- Add the digit check
- Run tests — show GREEN

---

## Exercise 4

- Write a test: password with no special character returns `{ valid: false }`
- Run tests — show RED
- Add the special character check
- Run tests — show GREEN
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

## Live Refactoring

### Refactor 1 — `fail()` helper

- Extract `const fail = message => ({ valid: false, message })`
- Replace all four return sites
- Run tests — still green

### Refactor 2 — Extract `getViolations()`

- Extract `getViolations(password)` that collects error strings into an array
- `validatePassword` wraps the result
- Run tests — still green
- Point out: `getViolations` now has one job and is independently testable

### Refactor 3 — Collect all errors (KEY MOMENT)

- New requirement: show all errors at once, not just the first
- Update the tests first — change expected shape to `{ valid: false, errors: [...] }`
- Run tests — RED (tests drive the change)
- Update implementation to return all violations
- Run tests — GREEN
- Point out: the test changed before the implementation — TDD handles requirement changes the same way it handles new code

---

## TDD Best Practices

- Reduce mocking and stubbing
- Avoid testing private/internal code; focus on public interfaces
- Avoid Over-Testing

---

## More on TDD

- [TDD, Where Did It All Go Wrong](https://www.youtube.com/watch?v=EZ05e7EMOLM)
- [Jim Coplien and Bob Martin Debate TDD](https://www.youtube.com/watch?v=KtHQGs3zFAM)
