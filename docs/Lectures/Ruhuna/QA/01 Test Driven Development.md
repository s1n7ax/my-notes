# Test Driven Development

by Srinesh Nisala

- LinkedIn: [https://www.linkedin.com/in/srinesh-nisala/](https://www.linkedin.com/in/srinesh-nisala/)
- GitHub: [https://github.com/s1n7ax](https://github.com/s1n7ax)

---

## Pre-requisites

- Create a Github account
- Get a fork of [https://github.com/s1n7ax/lecture_qa](https://github.com/s1n7ax/lecture_qa)
- Open the project with Codespace

---

## Project structure

- Explain how to run the application using IDE & Gradle

```shell
# with gradle
gradle run

# with gradle wrapper
./gradlew run
```

- Explain how to run tests using IDE & Gradle

```shell
# with gradle
gradle test --info
          # ^^^ by default stdout is not shown when running tests
          # --info flag shows the output

# with gradle wrapper
./gradlew test
```

---

## Basics of JUnit

- Create a simple test to print hello world (check the output in the debug console tab)

- Introduce `beforeEach` and `afterEach` annotations

---

## Exercise 1

- Create a `Calculator` class and add `addition` method
- Show how to use IDE features to quickly create a test class
- Tryout the `addition` method manually
- Create a unit test to test the `addition` method

---

## Exercise 2

- Create a test case for `subtraction` method
- Use IDE features to generate the method signature
- Implement the `subtraction` method

---

## What is TDD?

- Describe the behaviour, then implement

---

## Random

- Do not test implementation details test behaviours
