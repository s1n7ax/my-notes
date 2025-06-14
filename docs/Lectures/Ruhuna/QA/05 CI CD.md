# CI CD

By Srinesh Nisala

- LinkedIn: [https://www.linkedin.com/in/srinesh-nisala/](https://www.linkedin.com/in/srinesh-nisala/)
- GitHub: [https://github.com/s1n7ax](https://github.com/s1n7ax)

---

## Exercise 1

### Pre-requisites

- Get a fork of [https://github.com/s1n7ax/lecture-cicd](https://github.com/s1n7ax/lecture-cicd)
- Go to the fork, click on `Actions` tab and enable Github Actions
- Open the repository in Codespaces

---

### 1) Performing actions on Linux

- `echo`: Prints text to the console
- `pwd`: Current directory we are in
- `ls`: List files

---

### 2) Replicate these action on GitHub Actions

- Open the `.github/workflows/test.yaml` file in Codespaces
- Add commands to run in the workflow
- Commit and push the changes

---

### 3) Run UI tests in local machine

- Clone the repository to your local machine
- Open the project and explain the content
- Explain the headless mode of UI tests
- Run `gradle test` or `./gradle test`

---

### 4) Run UI tests in GitHub Actions

- Open the `.github/workflows/test.yaml` and add test run action
- Try failing the test

## Theory

[Introduction to CI/CD](https://notes.s1n7ax.com/docs/Lectures/Intruduction%20to%20CICD)
