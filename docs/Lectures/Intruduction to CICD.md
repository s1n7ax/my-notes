---
title: Introduction to CI/CD - Building Modern Development Pipelines
author: By Srinesh Nisala
---

# Agenda

1. What is Continuous integration (CI)?
1. What is Continuous Delivery/Deployment (CD)?
1. Why CI/CD Matters
1. Key Components of CI/CD
1. Tools for CI/CD
1. Career Path
1. Q&A

---

# What is CI?

> Continuous integration is a DevOps software development practice where developers regularly merge their code changes into a central repository, after which automated builds and tests are run. Continuous integration most often refers to the build or integration stage of the software release process and entails both an automation component (e.g. a CI or build service) and a cultural component (e.g. learning to integrate frequently)

> [!TIP]
> Break the big tasks to smaller sub tasks
> More automated less manual

> [!TIP]
> The term `job` is used for a small unit of work while `pipeline` is a sequence of `jobs` in a specific order

---

## Platforms for CI

- **GitHub Actions** - GitHub Actions is a product feature that lets you automate workflows with code
- **Jenkins** - Jenkins is an open source automation server
- **Azure DevOps** - Azure DevOps is a platform that supports software development with cloud or on-premises services
- **AWS CodePipeline** - AWS CodePipeline is a continuous delivery service that enables you to model, visualize, and automate the steps required to release your software.

---

## What do we do in CI jobs

- Secrets scanning
- Code formatting checks
- Code lint
- Dependency vulnerabilities
- Tests
- Build (build release artifacts)

---

## Examples

### Vercel lint pipeline

[source](https://github.com/vercel/vercel/blob/cc8c08e4688df1e76805614bf1c28b69e9f3f7a5/.github/workflows/test-lint.yml#L41-L52)

![vercel lint](../assets/2025-01-01-12-49-47.png)

---

### nvim-java releases

[source](https://github.com/nvim-java/nvim-java/blob/e8e84413ca03e7d0541921e795b2e6bf8801f186/.github/workflows/release.yml?plain=1#L11-L18)

![nvim-java release](../assets/2025-01-01-12-33-52.png)

---

### Home Assistant vulnerability check

[source](https://github.com/home-assistant/core/blob/2e1463b9e9515a0a9413794a1efe7f66269a731e/.github/workflows/codeql.yml#L22-L34)

![home assistant code quality](../assets/2025-01-01-12-56-25.png)

---

# What is CD

> Continuous delivery is a software development practice where code changes are automatically prepared for a release to production. A pillar of modern application development, continuous delivery expands upon continuous integration by deploying all code changes to a testing environment and/or a production environment after the build stage

- **Continuous Deployment/Delivery (CD):**
  - **Deployment:** Fully automated release of code to production.
  - **Delivery:** Automation up to a manual release checkpoint.

---

# Demo

---

# Why CI/CD Matters

- **Faster Development Cycles:** Code changes deployed rapidly.
- **Improved Collaboration:** Ensures consistent code quality across teams.
- **Early Bug Detection:** Tests catch issues before reaching production.
- **Reliability:** Automates repetitive tasks, reducing human error.
- **Scalability:** Efficient workflows that grow with the team.

---

# Key Components of CI/CD

- **Version Control Systems:** Git, GitHub, GitLab.
- **Build Automation:** Tools like Jenkins, GitHub Actions.
- **Testing Frameworks:** JUnit, Selenium, PyTest.
- **Deployment Automation:** Docker, Kubernetes, Terraform.
- **Monitoring Tools:** Prometheus, Grafana, Datadog.

---

# Popular CI/CD Tools

- **Jenkins**: Open-source CI tool with extensive plugin support.
- **GitHub Actions**: Native CI/CD for GitHub repositories.
- **GitLab CI/CD**: Integrated tool for GitLab repositories.
- **CircleCI**: Cloud-based CI/CD for fast pipeline setups.
- **Travis CI**: Popular for open-source projects.

---

# Building Your First CI/CD Pipeline

---

## Step 1: Set Up a Repository

- Create a GitHub repository for your project.
- Add a sample codebase (e.g., a simple Python/JavaScript app).

---

## Step 2: Write a Build Script

- Example: For Python, create a `requirements.txt` and a `test.py` file.
- `test.py`:

```python
def test_addition():
    assert 1 + 1 == 2
```

---

## Step 3: Configure a CI/CD Tool

- **Example:** GitHub Actions

  - Add a `.github/workflows/main.yml` file:

```yaml
name: CI Pipeline

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set Up Python
        uses: actions/setup-python@v4
        with:
          python-version: "3.x"

      - name: Install Dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Run Tests
        run: pytest
```

---

## Step 4: Test the Pipeline

- Push code to GitHub and watch the pipeline execute.
- Fix any issues reported in the logs.

---

## Step 5: Add Deployment

- Use a service like AWS, Heroku, or Netlify for deploying the application.

---

# Best Practices

- Commit frequently to keep changes small and manageable.
- Write clear and comprehensive tests.
- Secure sensitive data with environment variables.
- Monitor and analyze CI/CD pipelines for performance.
- Regularly update and maintain the pipeline configuration.

---

# Practical Tips for Students

- Start with a simple CI/CD setup using GitHub Actions.
- Explore Docker to containerize your applications.
- Experiment with free-tier cloud services for deployment.
- Collaborate with peers to understand team workflows.
- Use public repositories to showcase your CI/CD knowledge.

---

# Q&A

- Open the floor for questions.
- Suggested topics: Debugging pipelines, choosing tools, learning resources.

# Career Path

| Role                      | ELI5 Explanation                                                  |
| ------------------------- | ----------------------------------------------------------------- |
| System Administrator      | Do more maintainance work and make sure applications is available |
| DevOps Engineer           | Build architecture to make sure everything running smoothly       |
| Site Reliability Engineer | Ensures the reliability, scalability, and performance             |

---

## Salaries

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->

![](../assets/2025-01-02-04-50-42.png)

<!-- column: 1 -->

![](../assets/2025-01-02-04-51-33.png)

---

## DevOps

> DevOps is the combination of cultural philosophies, practices, and tools that increases an organization’s ability to deliver applications and services at high velocity

### Core Responsibilities

- Automation and CI/CD Pipelines (Jenkins, GitLab CI, GitHub Actions)
- Infrastructure Management (Terraform, Ansible, or CloudFormation)
- Monitoring and Logging (Prometheus, Grafana, Datadog, ELK Stack)
- Performance Optimization
- Incident Response

### Skills Required

- Technical Skills

  - Proficiency in Linux/Unix administration.
  - Knowledge of programming and scripting languages like Python, Bash, or Go.
  - Experience with version control systems, e.g., Git.

- Cloud Platforms

  - Experience with AWS, Azure, GCP, or other cloud providers.
  - Understanding of containerization using Docker and orchestration with Kubernetes

- Tooling Expertise

  - CI/CD tools (e.g., Jenkins).
  - Configuration management tools (e.g., Ansible, Puppet).
  - Monitoring tools (e.g., Nagios, Prometheus).

---
