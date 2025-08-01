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

