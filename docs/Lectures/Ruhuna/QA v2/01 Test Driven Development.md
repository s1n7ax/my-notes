# Test Driven Development

By Srinesh Nisala (Senior Software Engineer @ iLabs)

- [LinkedIn](https://www.linkedin.com/in/srinesh-nisala/)
- [Github](https://github.com/s1n7ax)

---

## 1. Introduction to Vitest

**Objective:** Explore Vitest as a unit testing tool.

### Key Topics

- **What a test file looks like:**
  - `describe()`, `it()` and `expect()`
- **Sanity check:**
  - Write a simple passing test to confirm the setup works

---

## 2. Hands-On Demo: Building a Password Validator with TDD

**Objective:** Implement a TDD workflow using Vitest.

### Pre-requisites

- Create a Github account
- Get a fork of [https://github.com/s1n7ax/lecture-tdd-v2](https://github.com/s1n7ax/lecture-tdd-v2)
- Open the project with Codespace

### Understanding the project structure

- Explain how to run tests

```shell
npm test
```

### Write all tests first

- Create `password.js` and `password.test.js`
- Write a test: short password returns `{ valid: false }`
- Write a test: 8-char password returns `{ valid: true }`
- Write a test: password with no uppercase returns `{ valid: false }`
- Write a test: password with no digit returns `{ valid: false }`
- Write a test: password with no special character returns `{ valid: false }`
- Run all tests — show all RED

### Exercise

1. **Minimum length** — Implement minimum code: check `password.length >= 8`. Run tests — first two GREEN, rest still RED
2. **Uppercase** — Add the uppercase check (`/[A-Z]/`). Run tests — show GREEN
3. **Digit** — Add the digit check (`/[0-9]/`). Run tests — show GREEN
4. **Special character** — Add the special character check (`/[^a-zA-Z0-9]/`). Run tests — all GREEN. Point out the smell: `{ valid: false, message }` repeated four times

---

## 3. Introduction to TDD

**Objective:** Understand the philosophy and purpose of TDD.

### Key Topics

- **What is TDD?**
  - Test-Driven Development (TDD) is a Software development method in which you write Automation Tests before the actual development process starts.
- **Red-Green-Refactor:**
  - Focus on testing behaviors (requirements) rather than implementation details.
  - Write minimal code to pass tests ("green").
  - Refactor without adding new tests.
- **Pros:**
  - Forces you to think about the interface before the implementation.
  - Tests act as living documentation — they show exactly what the code is supposed to do.
  - Gives confidence to refactor without breaking existing behaviour.
- **Cons:**
  - Can give false confidence if tests only cover happy paths.
- **Best Practices:**
  - Never write code without a failing test: You may only write new production code to pass a unit test that has already failed.
  - Write minimal tests: Do not write more of a test than is necessary to fail. Compilation failures are considered test failures.
  - Code to pass: Write exactly the amount of production code needed to satisfy the failing test, not more.

![](../../../../assets/red-green-refactor.png)

### 4. References

- [TDD, Where Did It All Go Wrong](https://www.youtube.com/watch?v=EZ05e7EMOLM)
- [Jim Coplien and Bob Martin Debate TDD](https://www.youtube.com/watch?v=KtHQGs3zFAM)
