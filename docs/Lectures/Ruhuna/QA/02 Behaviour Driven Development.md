# Behaviour Driven Development

By Srinesh Nisala

- [LinkedIn](https://www.linkedin.com/in/srinesh-nisala/)
- [Github](https://github.com/s1n7ax)

---

## 1. Introduction to Cucumber

**Objective:** Explore Cucumber as a BDD tool.

### Key Topics

- **What is Cucumber?**
  - Open-source tool supporting BDD with plain-language specifications.
  - Uses Gherkin syntax to write scenarios.
- **Gherkin Syntax Basics:**
  - Keywords:
    - `Feature`: description of a software feature
    - `Scenario`: example that illustrates a business rule
    - `Given`: initial context of the system
    - `When`: describe an event, or an action
    - `Then`: describe an expected outcome
- **Tool Integration:** Works with Java, Ruby, JavaScript, etc., via frameworks like JUnit or Selenium.

```gherkin
Scenario: eat 5 out of 12
  Given there are 12 cucumbers
  When I eat 5 cucumbers
  Then I should have 7 cucumbers
```

---

## 2. Hands-On Demo: Building a Feature with Cucumber

**Objective:** Implement a BDD workflow using Cucumber.

### Pre-requisites

- Get a fork of [https://github.com/s1n7ax/lecture-bdd](https://github.com/s1n7ax/lecture-bdd)
- Run the project in Codespace

### Understanding the project structure

- Explain `package.json`
- Explain feature
- Explain step definition

### Exercise

1. Parameterize the addition test without hard-coded values
2. Write a scenario for subtraction
3. Write step definition for subtraction
4. Implement subtraction feature to calculator
5. Instead of hard-coded values, parameterize the values

---

## 3. Introduction to BDD

**Objective:** Understand the philosophy and purpose of BDD.

### Key Topics

- **What is BDD?**
  - Agile methodology bridging technical and non-technical stakeholders.
  - Evolved from TDD (Test-Driven Development) but focuses on _behavior_ over tests.
  - **Key Goal:** Ensure software meets business requirements through collaboration.
- **Why BDD?**
  - Reduces misunderstandings between developers, testers, and product owners.
  - Creates living documentation (executable specifications).
  - Encourages iterative, example-driven development.
- **BDD vs. TDD:**
  - TDD: "Write tests first, then code." Focuses on code correctness.
  - BDD: "Define behavior first, then automate." Focuses on business value.
