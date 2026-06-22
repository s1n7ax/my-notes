---
title: Introduction to QA Automation
author: By Srinesh Nisala
---

# Introduction to QA Automation

> All automation is written in **JavaScript** and runs in **GitHub Codespaces** — no local setup.

This lecture covers what automated testing is, the three **interfaces** we write tests through
(functions, API, UI), and the **types** of tests you'll hear about in industry.

Repo: **https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2** · [old lecture notes](https://github.com/s1n7ax/lecture-intro-to-qa-automation)

---

## 0. Getting started

1. Open the repo above, then **`<> Code` → `Codespaces` → `Create codespace on main`**.
2. Wait ~1–2 minutes — the Codespace auto-runs `npm install && npx playwright install --with-deps chromium`.
3. Open a terminal (`` Ctrl+` ``) and run `npm run test:unit`. Green checkmarks mean you're ready.

| Command | What it runs |
|---|---|
| `npm run test:unit` | Unit tests (Vitest) |
| `npm run test:api`  | API tests (Vitest + fetch) |
| `npm run test:ui`   | UI tests (Playwright) |
| `npm run test:ui:report` | Open the last UI test report |

---

## 1. What is test automation?

Testing checks that software does what it should. Instead of a human clicking through the app every
release, you **automate** it: write code that exercises the app and **asserts** the result, then run
it on demand in seconds.

Why automate? **Speed** (hundreds of checks in seconds), **regression safety** (catch what you broke
today), and it **runs in CI** on every push.

A test is always the same shape:

```
ARRANGE  set up the inputs / open the page
ACT      call the function / click the button
ASSERT   check the result is what you expected
```

---

## 2. The three interfaces (hands-on)

We write automation against three **interfaces**, from fastest to most realistic: a **function**
(call it directly), an **API** (over HTTP), and the **UI** (drive a real browser).

### 2a. Functions — `Vitest`

Test a **pure function** directly, no browser or network. The code under test (`src/cart.js`):

```js
export function applyDiscount(amount, percent) {
  if (percent < 0 || percent > 100) {
    throw new Error(`Discount percent must be between 0 and 100, got ${percent}`);
  }
  return amount - amount * (percent / 100);
}
```

The test (`tests/unit/cart.test.js`) — including the **error case**:

```js
import { describe, it, expect } from 'vitest';
import { applyDiscount } from '../../src/cart.js';

it('takes the right amount off', () => {
  expect(applyDiscount(100, 20)).toBe(80);
});

it('rejects a discount above 100%', () => {
  expect(() => applyDiscount(100, 150)).toThrow();
});
```

> **🖥️ Demo:** `npm run test:unit`. Break `src/cart.js` (`-` → `+`) and rerun to see a test go red.

**Takeaway:** unit tests are fast and precise — they pinpoint the exact function that's wrong.

### 2b. API — `fetch` + `Vitest`

Skip the UI and test the **backend contract** over HTTP, against the public
**[Swagger Petstore](https://petstore.swagger.io/)**. APIs describe themselves with an
**OpenAPI/Swagger spec**, which also powers the **Swagger UI** ("Try it out").

```js
it('GET /pet/findByStatus returns a list of available pets (200)', async () => {
  const res = await fetch('https://petstore.swagger.io/v2/pet/findByStatus?status=available');
  expect(res.status).toBe(200);
  const pets = await res.json();
  expect(Array.isArray(pets)).toBe(true);
});
```

> **🖥️ Demo:** open **https://petstore.swagger.io/**, expand `GET /pet/findByStatus` →
> **Try it out → Execute**. Then `npm run test:api` hits the same endpoint in code.

**Takeaway:** API tests are fast and don't depend on the UI — ideal for business logic and contracts.

### 2c. UI — `Playwright`

Drive a **real browser** like a user, using **[Playwright](https://playwright.dev/)** against
**[the-internet.herokuapp.com](https://the-internet.herokuapp.com/login)**. Playwright **auto-waits**
for elements, which makes tests far less flaky.

```js
import { test, expect } from '@playwright/test';

test('valid login lands on the secure area', async ({ page }) => {
  await page.goto('/login');
  await page.fill('#username', 'tomsmith');
  await page.fill('#password', 'SuperSecretPassword!');
  await page.click('button[type="submit"]');

  await expect(page).toHaveURL(/.*secure/);
  await expect(page.locator('#flash')).toContainText('You logged into a secure area!');
});
```

> **🖥️ Demo:** `npm run test:ui`, then `npm run test:ui:report` for the trace and screenshots.

**Takeaway:** UI tests are the most realistic but slowest — use them for critical journeys, not everything.

---

## 3. Types of tests

These are the words you'll see in job ads and tickets — **what** you're testing and **why**, not the
tool. Many are automated through the same three interfaces above.

### Unit — *Developer*

One function or class in isolation.

![Unit test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/unit-test-example-from-ms-calculator.png)

### Integration — *Developer*

Several units working together.

![Integration test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/integration-test-example-from-neovim.png)

### Smoke — *QA*

"Does the build even launch?"

![Smoke test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/smoke-test-example-from-vscode.png)

### Performance — *QA*

Speed and responsiveness under normal use.

![Performance test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/performance-test-from-chrome-lighthouse-for-google.png)

### Load — *QA*

Behaviour under heavy/concurrent traffic.

![Load test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/load-test-example-from-Anton-Putra-youtube.png)

### Security — *Security / QA*

Vulnerabilities and misuse.

![Security test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/security-test-example-with-zap.png)

### End-to-End — *QA*

A whole user journey across the system.

![E2E test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/e2e-test-example-from-peertube.png)

### UI — *QA*

The interface behaves and looks right.

![UI test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/ui-test-example-from-meteor.png)

### API — *QA*

Endpoints honour their contract.

![API test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/api-test-example-from-jsonplaceholder.png)

### Visual regression — *QA*

The UI didn't change pixels unexpectedly.

![Visual regression test example](https://github.com/s1n7ax/lecture-intro-to-qa-automation-v2/raw/main/assets/visual-regression-test-example-from-resemblejs.png)

> **Functional**, **regression**, and **acceptance** testing describe **intent**, not a tool — any of
> the tests above can serve those goals depending on what you're checking.

---

## 4. 🙌 Your turn — practical (~5 min)

You've seen a **valid** login test. Now write one for an **invalid** login (**negative testing**).

1. Open **`tests/ui/practical.spec.js`** and follow the `// TODO` comments:
   - fill `#username` with `wronguser`, `#password` with `wrongpass`, click submit
   - assert `#flash` contains **`Your username is invalid!`**
2. Run `npm run test:ui`. Stuck? The answer is in `solutions/practical.solution.spec.js`.

**Bonus:** also assert the page is still on `/login` (the user was *not* let in).

---

## 5. Recap

- A test is always **arrange → act → assert**.
- We automate through three **interfaces**, trading speed for realism:
  - **Functions** (Vitest) — instant, isolates logic.
  - **API** (fetch + Vitest) — fast, checks the backend contract.
  - **UI** (Playwright) — realistic, drives a real browser.
- Test **types** (unit, integration, smoke, performance, security, …) describe *what & why*.

### Go further
- Vitest — https://vitest.dev/
- Playwright — https://playwright.dev/
- Swagger / OpenAPI — https://swagger.io/
- Practice targets — https://the-internet.herokuapp.com/ · https://petstore.swagger.io/
