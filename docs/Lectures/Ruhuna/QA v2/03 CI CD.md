---
title: CI/CD
author: By Srinesh Nisala
---

# CI/CD

This lecture takes the **same repo** you used for QA Automation and makes its tests run
**automatically on every push** using **GitHub Actions**. We'll build a workflow **live**, step by
step, and watch it run the unit, API, and UI tests in the cloud.

Repo: **https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2**

[old lecture notes](https://notes.s1n7ax.com/docs/Lectures/Intruduction%20to%20CICD)

---

## 0. Getting started

1. **Fork** the repo above, then on your fork open the **`Actions`** tab and click **`I understand
   my workflows, go ahead and enable them`**.
2. Open the fork in a Codespace: **`<> Code` → `Codespaces` → `Create codespace on main`**.
3. In a terminal (`` Ctrl+` ``), run `npm run test:unit` to confirm tests pass locally first.

---

## 1. What is CI/CD?

- **CI — Continuous Integration:** every push **builds and tests** the code automatically, so you
  catch breakage in minutes instead of at release.
- **CD — Continuous Delivery/Deployment:** once the checks are green, the build is automatically
  **shipped** (to staging, or all the way to production).

Today we focus on the **CI** half: run our whole test suite on every push. The thing that runs it is
a **GitHub Actions workflow** — a YAML file in `.github/workflows/`.

---

## 2. A workflow is just commands on a Linux machine

GitHub gives us a fresh Linux VM (a **runner**). A workflow is the list of commands to run on it.
The shape:

```
on:        WHEN to run   (e.g. on every push)
jobs:      WHAT to run   (one or more jobs)
  steps:   the commands, top to bottom
```

> **🖥️ Demo:** in the Codespace terminal, run `echo hello`, `pwd`, `ls`. These are exactly the kind
> of commands a runner executes — a workflow just lists them for a machine in the cloud.

---

## 3. Build it live — first workflow

Create **`.github/workflows/ci.yaml`** and start with the Linux commands from above:

```yaml
name: CI

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Workflow is running 🎉"
      - run: pwd
      - run: ls
```

**Commit and push.** Open the **`Actions`** tab → click the run → expand the steps and read the
output. Notice `ls` shows an **empty** directory — the runner doesn't have our code yet.

---

## 4. Get the code and the tools

To run tests, the runner needs our **code**, **Node**, and the **dependencies**. Add three steps —
these use prebuilt **actions** (`uses:`) instead of raw commands:

```yaml
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm install
      - run: npx playwright install --with-deps chromium
```

> **🖥️ Demo:** push again. Now the `ls` from before would show our project — `checkout` pulled the
> repo onto the runner.

---

## 5. Run all the tests

Add the three test commands — the same ones you ran locally:

```yaml
      - run: npm run test:unit
      - run: npm run test:api
      - run: npm run test:ui
```

Push, open the run, and watch each step go **green**. The whole suite — functions, API, and a real
browser — just ran in the cloud with **no one clicking anything**. That's CI.

The full file:

```yaml
name: CI

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm install
      - run: npx playwright install --with-deps chromium
      - run: npm run test:unit
      - run: npm run test:api
      - run: npm run test:ui
```

---

## 6. Make it fail (this is the point)

CI is only useful if it **stops bad code**. Break a test on purpose:

1. In `src/cart.js`, change the discount math (e.g. `-` → `+`).
2. Commit and push.
3. Watch the run turn **red** ❌, get an **email**, and see the ✗ next to your commit.

A failing check is a **gate** — it tells you (and reviewers) the code isn't safe to merge. Revert the
change and watch it go green again.

---

## 7. 🙌 Your turn — practical (~5 min)

Make CI run on **pull requests** too, not just direct pushes:

1. Change the trigger to:
   ```yaml
   on:
     push:
     pull_request:
   ```
2. Create a branch, push it, and open a **Pull Request**.
3. See the **checks** appear on the PR — green means safe to merge, red means blocked.

**Bonus:** add a **branch protection rule** requiring the CI check to pass before merging.

---

## 8. Recap

- **CI** runs your build + tests automatically on every push; **CD** ships the green build.
- A **workflow** (`.github/workflows/*.yaml`) is just **`on:` (when)** + **`jobs`/`steps` (what)**,
  run on a fresh Linux runner.
- We built ours up live: **checkout → setup-node → install → run unit/API/UI tests**.
- A **failing check is a gate** — it keeps broken code from merging.

### Go further

- GitHub Actions — https://docs.github.com/en/actions
- Workflow syntax — https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions
- Marketplace actions — https://github.com/marketplace?type=actions
