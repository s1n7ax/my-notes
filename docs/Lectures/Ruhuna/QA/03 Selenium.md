# Selenium

**tldr;** Instead of using mouse and keyboard to control browser, you call a Selenium function.

> Selenium is a software project that allows you to automate web applications using various browsers

---

## Components of Selenium

ELI5 description

- **Web Driver** - jar file with bunch of classes to automate browser
- **Selenium IDE** - records actions you perform on browser and creates an automation script
- **Selenium Grid** - Run tests remotely

![Selenium components](assets/selenium-components.png)

---

## Selenium IDE hands on

> [!NOTE]
> Scripts created by this plugin is pretty terrible
> Not necessarily because it's bad engineering
> It's genuinely a hard problem

- Download and install the [Selenium IDE](https://www.selenium.dev/selenium-ide) (4MB)
- Create a new project
- Start a new recording with [https://demoqa.com/text-box](https://demoqa.com/text-box)
- Export the recorded script to a Java JUnit file

> [!NOTE]
> Generated code is using JUnit 4

---

## Selenium Web Driver hands on

### Pre-requisites

- Java 21
- Gradle 8
- Firefox
- VSCode with **Extension Pack for Java** (or any other Java IDE)

---

## Step 1 - Setting up Java project for test

[changes](https://github.com/s1n7ax/lecture-intro-to-qa-automation/compare/main...step-1)

- Create a new Java project

```bash
gradle init
```

---

## Step 2 - Google page load test

[changes](https://github.com/s1n7ax/lecture-intro-to-qa-automation/compare/step-1...step-2)

- Add selenium as dependency

```groovy
# app/build.gradle
testImplementation 'org.seleniumhq.selenium:selenium-java:4.27.0'
```

- Add a sample test

```java
@Test
void appHasAGreeting() {
  var browser = new FirefoxDriver();
  browser.get("https://www.google.com");

  // this is the test
  assertEquals(browser.getTitle(), "Google");
  browser.close();
}
```

---

## Webdriver classic, WebDriver BiDi

```shell
Dec 21, 2024 9:12:29 AM org.openqa.selenium.firefox.FirefoxDriver <init>
WARNING: CDP support for Firefox is deprecated and will be removed in future versions. Please switch to WebDriver BiDi.
```

### WebDriver classic architecture

<style scoped>img { width: 45%; }</style>

![webdriver classic architecture](assets/webdriver-classic-architecture.png)

### WebDriver BiDi architecture

![webdriver bidi architecture](assets/webdriver-bidi-architecture.png)

---

### Enable BiDi

#### Chrome

```java
var options = new ChromeOptions();
options.setCapability("webSocketUrl", true);
browser = new ChromeDriver(options);
```

#### Firefox

```java
var options = new FirefoxOptions();
options.setCapability("webSocketUrl", true);
browser = new FirefoxDriver(options);
```

---

## (Off topic) Remove extensions

> [!NOTE]
> While most Selenium commands are included in the specification, some things are browser specific

### On Chrome

```java
var options = new ChromeOptions();
options.addArguments("--disable-extensions");
browser = new ChromeDriver(options);
```

### On Firefox

```java
var options = new FirefoxOptions();
options.addArguments("--safe-mode");
browser = new FirefoxDriver(options);
```

> [!NOTE]
> --safe-mode flag in Firefox disables multiple features including extensions
> Such as Hardware Acceleration & Themes etc

---

## Step 3 - DemoQA form validation

<style scoped>
.cc {
  display: grid;
  grid-template-columns: 3fr 5fr;
  gap: 1rem;
  height: 50%;
}
</style>

[changes](https://github.com/s1n7ax/lecture-intro-to-qa-automation/compare/step-2...step-3)

- Manually check the website [https://demoqa.com/text-box](https://demoqa.com/text-box)
- Inspect the element in the form and output
- Capture the element to execute actions
- Validate the data after submit

<div class="cc">

```java
@BeforeEach
public void beforeEach() {
  var options = new FirefoxOptions();
  options.addArguments("--safe-mode");
  options.setCapability("webSocketUrl", true);
  browser = new FirefoxDriver(options);
}
```

```java
browser.get("https://demoqa.com/text-box");
var pageHeader = browser.findElement(By.tagName("h1"));
assertEquals(pageHeader.getText(), "Text Box");

browser.findElement(By.id("userName")).sendKeys("Srinesh Nisala");
browser.findElement(By.id("userEmail")).sendKeys("random@gmail.com");

var submitBtn = browser.findElement(By.id("submit"));
((JavascriptExecutor) browser).executeScript("arguments[0].scrollIntoView(true);", submitBtn);
submitBtn.click();

var output = browser.findElement(By.id("output"));
var acName = output.findElement(By.id("name")).getText();
var acEmail = output.findElement(By.id("email")).getText();

assertTrue(acName.endsWith("Srinesh Nisala"));
assertTrue(acEmail.endsWith("random@gmail.com"));
```

</div>

---

## Common Exceptions

ELI5 description;

- `NoSuchElementException` - Element you are looking for is not in the webpage. If selector is correct, see if it's inside an iframe
- `StaleElementReferenceException` - Element was there but not right now
- `ElementClickInterceptedException` - Popup probably covering the element or not in the view

> [!TIP]
> Looking for info? Search in [documentation](https://www.selenium.dev/documentation) first
> Then try GPTing it or try Stackoverflow

---

## Step 4 - Page object model design pattern

[changes](https://github.com/s1n7ax/lecture-intro-to-qa-automation/compare/step-3...step-4)

### Why page object model

- Re-usability
- Ease of maintenance
- Better readability and clarity

---

- Create pages from form and form output

<style scoped>
.cc {
  font-size:12px;
}
</style>

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->
<div class="cc">

```java
public class DemoQATextboxPage {
  private WebDriver browser;

  @FindBy(id = "userName")
  private WebElement fullName;

  @FindBy(id = "userEmail")
  private WebElement email;

  @FindBy(id = "submit")
  private WebElement submit;

  DemoQATextboxPage(WebDriver browser) {
    this.browser = browser;
    PageFactory.initElements(browser, this);
  }

  public void fillForm(String fullName, String email) {
    this.fullName.sendKeys(fullName);
    this.email.sendKeys(email);
    ((JavascriptExecutor) this.browser).executeScript("arguments[0].scrollIntoView(true);", this.submit);
    this.submit.click();
  }
}
```

<!-- column: 1 -->

```java
public class DemoQATextboxOutputPage {
  @FindBy(id = "name")
  private WebElement name;

  @FindBy(id = "email")
  private WebElement email;

  DemoQATextboxOutputPage(WebDriver browser) {
    var output = browser.findElement(By.id("output"));
    PageFactory.initElements(output, this);
  }

  public void validateForm(String expFullName, String expEmail) {
    assertTrue(this.name.getText().endsWith(expFullName));
    assertTrue(this.email.getText().endsWith(expEmail));
  }
}
```

</div>

---

# Step 5 - Data driven testing

<style scoped>
marp-pre {
  font-size: 16px;
}
</style>

[changes](https://github.com/s1n7ax/lecture-intro-to-qa-automation/compare/step-4...step-5)

Data-Driven Testing (DDT) is a software testing methodology in which test scripts execute a set of test cases using different sets of input data.

> [!NOTE]
> The following example demonstrates how to supply different data sets to tests, which is a crucial aspect of data-driven testing. However, it does not address handling varying scenarios based on the input data

```java
@ParameterizedTest
@ValueSource(strings = { "Srinesh,srinesh@email.com", "Nisala,nisala@email.com" })
void test(String detils) {
  browser.get("https://demoqa.com/text-box");

  var splitDetails = detils.split(",");
  var fullName = splitDetails[0];
  var email = splitDetails[1];

  DemoQATextboxPage.init(browser).fillForm(fullName, email);
  DemoQATextboxOutputPage.init(browser).validateForm(fullName, email);
}
```

---

# Step 6 - Headless mode

[changes](https://github.com/s1n7ax/lecture-intro-to-qa-automation/compare/step-5...step-6)

### Chrome

```java
var options = new ChromeOptions();
options.addArguments("--headless=new");
browser = new ChromeDriver(options);
```

### Firefox

```java
var options = new FirefoxOptions();
options.addArguments("--headless");
browser = new FirefoxDriver(options);
```

---

# Questions?
