# 🧪 Profile Creator: JavaScript + HTML Breakdown (with DOM Mapping)
(https://innersage.xyz/lab-based-guess-web/interactive)

This document offers **in-depth, line-by-line explanations** of how the HTML `<script>` section interacts with the page using DOM manipulation, user input, dynamic feedback, and styling.

---

## 🔗 JavaScript Element Selection & DOM Mapping

```js
const username = document.getElementById("username");
```
- **HTML Source**:
  ```html
  <input type="text" id="username" value="Oliver Brown" />
  ```
- **Purpose**: Grabs the input field for the user's name. It's used when submitting the profile and updating the display.

---

```js
const ageInput = document.getElementById("ageInput");
```
- **HTML Source**:
  ```html
  <input type="number" id="ageInput" placeholder="Enter an age above 10" />
  ```
- **Purpose**: Captures the age entered by the user. This value is parsed into a number for validation checks.

---

```js
const studyStatus = document.getElementById("studyStatus");
```
- **HTML Source**:
  ```html
  <input type="text" id="studyStatus" value="FT UG student" />
  ```
- **Purpose**: Used to reflect a study status (e.g., full-time, part-time). Displayed in the final profile card.

---

```js
const subscriptionType = document.getElementById("subscriptionType");
```
- **HTML Source**:
  ```html
  <select id="subscriptionType">
    <option value="standard">Standard £5.99 per month</option>
    <option value="premium">Premium £9.99 per month</option>
    <option value="basic">Basic £2.99 per month</option>
  </select>
  ```
- **Purpose**: Gets the selected subscription tier. Used in pricing logic and discount calculations.

---

```js
const membershipRadios = document.getElementsByName("membership");
```
- **HTML Source**:
  ```html
  <input type="radio" name="membership" value="annual" />
  <input type="radio" name="membership" value="monthly" checked />
  ```
- **Purpose**: Selects all radio buttons sharing the `name="membership"`. JavaScript uses `.checked` to determine if `annual` is selected.

---

```js
const feedback = document.getElementById("ageFeedback");
```
- **HTML Source**:
  ```html
  <div id="ageFeedback">Eligibility message will appear here</div>
  ```
- **Purpose**: Updates dynamically based on age validation and membership selection.

---

## 🧩 Display Section Mapping

```js
const resName = document.getElementById("resName");
const resStudy = document.getElementById("resStudy");
const resSub = document.getElementById("resSub");
```
- **HTML Source**:
  ```html
  <strong id="resName">[Your Name]</strong>
  <span id="resStudy">[Study Status]</span>
  <span id="resSub">[Your Subscription Choice]</span>
  ```
- **Purpose**: These are placeholders filled after clicking "Submit". They form the **live profile preview** card.

---

## 🎯 Buttons and Fields

```js
const submitBtn = document.getElementById("submitBtn");
const formFieldset = document.getElementById("formFieldset");
```
- **HTML Source**:
  ```html
  <button type="button" id="submitBtn">Submit Profile</button>
  <fieldset id="formFieldset">...</fieldset>
  ```
- **Purpose**: 
  - `submitBtn`: Listens for a click event to generate profile output.
  - `formFieldset`: The area where the background pattern updates.

---

## ✅ `validateEligibility()` Function

### 👇 Triggers when:
- User enters/changes age
- User selects annual/monthly membership

### 👇 Logic:
1. Reads the age from the input.
2. Checks which radio button is active.
3. If `annual` and age ≥ 18 → discount applies (green message)
4. If age between 11–17 → not eligible (red message)
5. If invalid or too young → warning (orange message)
6. If `monthly` → blue info message

- **HTML Affected**: `#ageInput`, `#ageFeedback`, radio buttons
- **CSS Impact**: `feedback.style.color`, `backgroundColor`, `borderColor`

---

## 🔘 Event Listeners

```js
ageInput.addEventListener("input", validateEligibility);
membershipRadios.forEach(r => r.addEventListener("change", validateEligibility));
```
- **Purpose**: Ensures the feedback is updated in real-time when the user modifies inputs.

---

## 🧾 Submit Profile Logic

```js
submitBtn.addEventListener("click", () => { ... });
```

- Extracts values from inputs
- Determines `basePrice` from subscription
- Applies **20% discount** if:
  - Annual membership is selected
  - Age ≥ 18
- Fills result preview via:
  ```js
  resName.textContent = name;
  resStudy.textContent = study;
  resSub.textContent = finalSubscription;
  ```

---

## 🎨 Background Pattern Logic

### Selectors:
```js
const thumb1 = document.getElementById("thumb1");
const thumb2 = document.getElementById("thumb2");
const thumb3 = document.getElementById("thumb3");
```

- **HTML**:
  ```html
  <div class="thumb" id="thumb1" style="background-image: url('images/pattern1.jpg');"></div>
  ```

### Logic:
- Each thumbnail triggers an event.
- `clearSelection()` resets all `.selected` classes.
- Updates `formFieldset.style.backgroundImage` dynamically.
- Enhances interactivity and user control of form visuals.

---

## 🟢 Final Initialization

```js
validateEligibility();
```

- Called once when the page loads to **immediately evaluate eligibility** based on default values.

---

## ✅ Summary

| Functionality         | HTML Element(s)        | JS Logic                       | UI Feedback       |
|----------------------|------------------------|--------------------------------|-------------------|
| Name input           | `#username`            | `username.value`               | → `#resName`      |
| Age validation       | `#ageInput`            | `validateEligibility()`        | → `#ageFeedback`  |
| Subscription logic   | `#subscriptionType`    | Dynamic price / discount logic | → `#resSub`       |
| Membership selection | `name="membership"`    | radio `.checked` check         | → JS Logic branch |
| Custom background    | `#thumb1/2/3`           | `formFieldset.style...`        | Visual styling    |

---

> 🎓 This script teaches DOM interaction, event-driven logic, real-time feedback, and basic pricing algorithms — ideal for lab-based or introductory frontend assignments.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>@thev1ndu/labs</title>
  <link rel="stylesheet" href="interactive.css">
</head>
<body>
  <main class="main-wrapper">
    <header>
      <h1>Profile Creator</h1>
      <p><strong>Thevindu W.</strong><br>Student ID: W2151910<br>BSc. Computer Science</p>
    </header>

    <form class="profile-form">
      <fieldset id="formFieldset">
        <legend>User Details</legend>

        <label>User Name:
          <input type="text" id="username" value="Oliver Brown" />
        </label>

        <label>Age:
          <input type="number" id="ageInput" placeholder="Enter an age above 10" />
        </label>
        <div id="ageFeedback">Eligibility message will appear here</div>

        <label>Study Status:
          <input type="text" id="studyStatus" value="FT UG student" />
        </label>

        <label>Subscription Type:
          <select id="subscriptionType">
            <option value="standard">Standard £5.99 per month</option>
            <option value="premium">Premium £9.99 per month</option>
            <option value="basic">Basic £2.99 per month</option>
          </select>
        </label>

        <div class="subscription-options">
          <label><input type="radio" name="membership" value="annual" /> Annual membership (20% Discount)</label>
          <label><input type="radio" name="membership" value="monthly" checked /> Monthly membership (No Discount)</label>
        </div>

        <button type="button" id="submitBtn">Submit Profile</button>
      </fieldset>
    </form>

    <section class="result-profile">
      <h2>Your Profile</h2>
      <div class="profile-card">
        <div class="profile-avatar" id="profileAvatar">ABC</div>
        <div>
          <p><strong id="resName">[Your Name]</strong></p>
          <p>Study: <span id="resStudy">[Study Status]</span></p>
          <p>Subscription: <span id="resSub">[Your Subscription Choice]</span></p>
        </div>
      </div>
    </section>

    <section class="customizer">
      <h3>Customization</h3>
      <p>Change the Background Pattern</p>
      <div class="thumbs">
        <div class="thumb" id="thumb1" style="background-image: url('images/pattern1.jpg');"></div>
        <div class="thumb" id="thumb2" style="background-image: url('images/pattern2.jpg');"></div>
        <div class="thumb" id="thumb3" style="background-image: url('images/pattern3.jpg');"></div>
      </div>
    </section>
  </main>

  <script>
    const username = document.getElementById("username");
    const ageInput = document.getElementById("ageInput");
    const studyStatus = document.getElementById("studyStatus");
    const subscriptionType = document.getElementById("subscriptionType");
    const membershipRadios = document.getElementsByName("membership");
    const feedback = document.getElementById("ageFeedback");

    const resName = document.getElementById("resName");
    const resStudy = document.getElementById("resStudy");
    const resSub = document.getElementById("resSub");

    const submitBtn = document.getElementById("submitBtn");
    const formFieldset = document.getElementById("formFieldset");

    let selectedMembership = "monthly";

    // Live feedback on age eligibility
    function validateEligibility() {
      const age = parseInt(ageInput.value);

      membershipRadios.forEach(radio => {
        if (radio.checked) selectedMembership = radio.value;
      });

      if (selectedMembership === "annual") {
        if (!isNaN(age)) {
          if (age >= 18) {
            feedback.textContent = "✔ You are eligible for discount";
            feedback.style.color = "white";
            feedback.style.backgroundColor = "green";
            feedback.style.borderColor = "green";
          } else if (age > 10) {
            feedback.textContent = "✘ You are not eligible for discount";
            feedback.style.color = "white";
            feedback.style.backgroundColor = "red";
            feedback.style.borderColor = "red";
          } else {
            feedback.textContent = "Please enter an age above 10";
            feedback.style.color = "white";
            feedback.style.backgroundColor = "orange";
            feedback.style.borderColor = "orange";
          }
        } else {
          feedback.textContent = "Please enter a valid age";
          feedback.style.color = "white";
          feedback.style.backgroundColor = "orange";
          feedback.style.borderColor = "orange";
        }
      } else {
        feedback.textContent = "Standard subscription selected";
        feedback.style.color = "white";
        feedback.style.backgroundColor = "#2196F3";
        feedback.style.borderColor = "#2196F3";
      }
    }

    // Trigger feedback on age or subscription change
    ageInput.addEventListener("input", validateEligibility);
    membershipRadios.forEach(r => r.addEventListener("change", validateEligibility));

    // Submit and display the profile
    submitBtn.addEventListener("click", () => {
      const name = username.value;
      const age = parseInt(ageInput.value);
      const study = studyStatus.value;
      const subType = subscriptionType.value;

      let finalSubscription = "";
      let basePrice = 0;

      if (subType === "standard") {
        basePrice = 5.99;
        finalSubscription = "Standard £5.99 per month";
      } else if (subType === "premium") {
        basePrice = 9.99;
        finalSubscription = "Premium £9.99 per month";
      } else if (subType === "basic") {
        basePrice = 2.99;
        finalSubscription = "Basic £2.99 per month";
      }

      membershipRadios.forEach(r => {
        if (r.checked && r.value === "annual") {
          if (!isNaN(age) && age >= 18) {
            const discountedPrice = (basePrice * 0.8).toFixed(2);
            if (subType === "standard") {
              finalSubscription = "Standard £" + discountedPrice + " per month (after 20% discount)";
            } else if (subType === "premium") {
              finalSubscription = "Premium £" + discountedPrice + " per month (after 20% discount)";
            } else if (subType === "basic") {
              finalSubscription = "Basic £" + discountedPrice + " per month (after 20% discount)";
            }
          } else {
            finalSubscription = finalSubscription + " (no discount available)";
          }
        }
      });

      resName.textContent = name;
      resStudy.textContent = study;
      resSub.textContent = finalSubscription;
    });

    // Background selector functionality
    const thumb1 = document.getElementById("thumb1");
    const thumb2 = document.getElementById("thumb2");
    const thumb3 = document.getElementById("thumb3");
    
    function clearSelection() {
      thumb1.classList.remove("selected");
      thumb2.classList.remove("selected");
      thumb3.classList.remove("selected");
    }

    // Event listeners
    thumb1.addEventListener("click", () => {
      clearSelection();
      thumb1.classList.add("selected");
      formFieldset.style.backgroundImage = "url('images/pattern1.jpg')";
      formFieldset.style.backgroundRepeat = "repeat";
      formFieldset.style.backgroundSize = "cover";
    });

    thumb2.addEventListener("click", () => {
      clearSelection();
      thumb2.classList.add("selected");
      formFieldset.style.backgroundImage = "url('images/pattern2.jpg')";
      formFieldset.style.backgroundRepeat = "repeat";
      formFieldset.style.backgroundSize = "cover";
    });

    thumb3.addEventListener("click", () => {
      clearSelection();
      thumb3.classList.add("selected");
      formFieldset.style.backgroundImage = "url('images/pattern3.jpg')";
      formFieldset.style.backgroundRepeat = "repeat";
      formFieldset.style.backgroundSize = "cover";
    });

    // Initialize
    validateEligibility();
  </script>
</body>
</html>
```
