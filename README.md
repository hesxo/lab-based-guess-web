# 🧪 Profile Creator

A responsive, interactive form that allows users to input their details, check eligibility for a subscription discount, and view their profile dynamically. Includes live JavaScript feedback, background customization via thumbnails, and a modern UI using plain HTML, CSS, and JavaScript.

---

## 🌐 HTML Breakdown

### ✅ 1. Page Setup

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Profile Creator</title>
```

📝 Sets the document to HTML5, sets the language to English, encodes characters in UTF-8, ensures responsiveness on mobile, and sets the tab title to “Profile Creator”.

---

### ✅ 2. Main Content Wrapper

```html
<main class="main-wrapper">
  <header>
    <h1>Profile Creator</h1>
    <p><strong>Student Full Name</strong><br>Student ID: W2142567<br>The course you study</p>
  </header>
```

📝 This section holds the header and all app content. It uses the `main-wrapper` class to center and style the content in a card-like box. The header contains student identification info.

---

### ✅ 3. Form Section

```html
<form class="profile-form">
  <fieldset id="formFieldset">
    <legend>User Details</legend>
```

📝 The `<form>` contains all input elements. The `<fieldset>` and `<legend>` group them semantically. The `id="formFieldset"` is used for background updates.

---

### ✅ 4. Input Fields

```html
<label>User Name:
  <input type="text" id="username" value="Oliver Brown" />
</label>

<label>Age:
  <input type="number" id="ageInput" placeholder="Enter an age above 10" />
</label>
<div id="ageFeedback">Eligibility message will appear here</div>
```

📝 Inputs for user name and age. The `ageInput` triggers JS validation. The `ageFeedback` displays eligibility info.

---

### ✅ 5. Select and Radio Options

```html
<label>Study Status:
  <select id="studyType">
    <option value="FT UG student">FT UG student</option>
    <option value="PT PG student">PT PG student</option>
  </select>
</label>

<label><input type="radio" name="membership" value="annual" /> Annual (20% discount if 18+)</label>
<label><input type="radio" name="membership" value="monthly" checked /> Monthly (no discount)</label>
```

📝 The user can choose their study type and select one of two subscription options using radio buttons.

---

### ✅ 6. Submit Button

```html
<button type="button" id="submitBtn">Submit Profile</button>
```

📝 This button triggers JavaScript to display the profile based on user inputs.

---

### ✅ 7. Profile Display Section

```html
<section class="result-profile">
  <h2>Your Profile</h2>
  <p><strong id="resName">[Your Name]</strong></p>
  <p>Study: <span id="resStudy">[Study Status]</span></p>
  <p>Subscription: <span id="resSub">[Your Subscription Choice]</span></p>
</section>
```

📝 When the form is submitted, these placeholders are replaced dynamically by JavaScript with actual values.

---

### ✅ 8. Background Customizer

```html
<section class="customizer">
  <p>Change the Background Pattern</p>
  <div class="thumbs">
    <div class="thumb" id="thumb1" style="background-image: url('images/pattern1.jpg');"></div>
    <div class="thumb" id="thumb2" style="background-image: url('images/pattern2.jpg');"></div>
    <div class="thumb" id="thumb3" style="background-image: url('images/pattern3.jpg');"></div>
  </div>
</section>
```

📝 Shows 3 circular thumbnails. When clicked, they update the background of the form’s fieldset.

---

## 🎨 CSS Breakdown

### ✅ 1. Page and Wrapper Styling

```css
body {
  font-family: 'Segoe UI', sans-serif;
  background: #eef1f4;
  padding: 30px;
}

.main-wrapper {
  background: #fff;
  max-width: 850px;
  margin: auto;
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 0 12px rgba(0,0,0,0.1);
}
```

📝 Styles the page background and centers a white card container with padding, rounded corners, and shadow.

---

### ✅ 2. Typography and Labels

```css
header p {
  font-style: italic;
  margin-bottom: 15px;
}

.profile-form label {
  display: block;
  margin-top: 15px;
}
```

📝 Italicizes header text and ensures proper spacing between form labels.

---

### ✅ 3. Feedback and Result Display

```css
#ageFeedback {
  margin: 5px 0 10px;
  font-weight: bold;
  border-bottom: 2px solid transparent;
}

.result-profile {
  margin-top: 25px;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background: #fafafa;
}
```

📝 The feedback div is styled for visibility. The result card mimics a clean summary box.

---

### ✅ 4. Thumbnail Customizer

```css
.thumb {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  margin-right: 12px;
  cursor: pointer;
  border: 2px solid transparent;
}

.thumb.selected {
  border: 2px solid green;
}
```

📝 Thumbnails are small, round, clickable buttons. The selected one is highlighted with a green border.

---

## ⚙️ JavaScript Breakdown

### ✅ 1. Age Eligibility Logic

```js
function validateEligibility() {
  const age = parseInt(ageInput.value);

  membershipRadios.forEach(radio => {
    if (radio.checked) selectedMembership = radio.value;
  });

  if (selectedMembership === "annual") {
    if (!isNaN(age)) {
      if (age >= 18) {
        feedback.textContent = "✔ You are eligible for discount";
        feedback.style.color = "green";
        feedback.style.borderColor = "green";
      } else {
        feedback.textContent = "✘ You are not eligible for discount";
        feedback.style.color = "red";
        feedback.style.borderColor = "red";
      }
    } else {
      feedback.textContent = "Please enter a valid age";
      feedback.style.color = "orange";
      feedback.style.borderColor = "orange";
    }
  } else {
    feedback.textContent = "Standard subscription selected";
    feedback.style.color = "orange";
    feedback.style.borderColor = "orange";
  }
}
```

🧠 **Where used:** Called on input events from `ageInput` and `membershipRadios`.  
🔍 **How it works:** Dynamically checks if age ≥ 18 and updates the feedback area accordingly. Uses `.textContent`, `.style.color`, and `.style.borderColor`.

---

### ✅ 2. Form Submission Display Logic

```js
submitBtn.addEventListener("click", () => {
  const name = username.value;
  const age = parseInt(ageInput.value);
  const study = studyType.value;

  let plan = "Standard £5.99 per month";

  membershipRadios.forEach(r => {
    if (r.checked && r.value === "annual") {
      if (!isNaN(age) && age >= 18) {
        plan = "Standard £" + (5.99 * 0.8).toFixed(2) + " per month (after 20% discount)";
      } else {
        plan = "Standard £5.99 per month (no discount)";
      }
    }
  });

  resName.textContent = name;
  resStudy.textContent = study;
  resSub.textContent = plan;
});
```

🧠 **Where used:** Triggered when the "Submit Profile" button is clicked.  
🔍 **How it works:** Captures inputs, checks discount eligibility, and populates the result card dynamically.

---

### ✅ 3. Background Selector Logic

```js
function clearSelection() {
  thumb1.classList.remove("selected");
  thumb2.classList.remove("selected");
  thumb3.classList.remove("selected");
}

thumb1.addEventListener("click", () => {
  clearSelection();
  thumb1.classList.add("selected");
  formFieldset.style.backgroundImage = "url('images/pattern1.jpg')";
  formFieldset.style.backgroundRepeat = "repeat";
  formFieldset.style.backgroundSize = "cover";
});
```

🧠 **Where used:** When a thumbnail is clicked.  
🔍 **How it works:** Clears previous selection, highlights the clicked one, and updates the form background via JS.

---

## 📦 Assets Required

- `images/pattern1.jpg`
- `images/pattern2.jpg`
- `images/pattern3.jpg`

Make sure these images exist in an `/images/` directory.

---

## ✅ Final Notes

- Built using only HTML, CSS, and JavaScript
- Mobile-friendly and responsive
- Can be extended with nickname generators, avatars, or theme switchers

---

## 📦 Full Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- ✅ Task 1: HTML Setup - Required Meta and Title -->
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Profile Creator</title>
  <style>
    /* ✅ Task 2.1: Style the whole document */
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #eef1f4;
      padding: 30px;
    }

    /* ✅ Task 2.2: Style the container */
    .main-wrapper {
      background: #fff;
      max-width: 850px;
      margin: auto;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 0 12px rgba(0,0,0,0.1);
    }

    /* Header content styling */
    header p {
      font-style: italic;
      margin-bottom: 15px;
    }

    /* Fieldset for form layout */
    fieldset {
      border: 2px solid #ccc;
      padding: 20px;
      border-radius: 10px;
      transition: background-color 0.3s ease;
    }

    legend {
      font-weight: bold;
      font-size: 1.1rem;
    }

    /* Form labels */
    .profile-form label {
      display: block;
      margin-top: 15px;
    }

    /* ✅ Task 3: Feedback styling for age eligibility */
    #ageFeedback {
      margin: 5px 0 10px;
      font-weight: bold;
      border-bottom: 2px solid transparent;
    }

    /* ✅ Task 4: Profile display card */
    .result-profile {
      margin-top: 25px;
      padding: 15px;
      border: 1px solid #ccc;
      border-radius: 8px;
      background: #fafafa;
    }

    /* ✅ Task 5: Background pattern thumbnails */
    .thumbs {
      display: flex;
      margin-top: 15px;
    }

    .thumb {
      width: 28px;
      height: 28px;
      border-radius: 50%;
      margin-right: 12px;
      cursor: pointer;
      border: 2px solid transparent;
    }

    .thumb.selected {
      border: 2px solid green; /* ✅ Highlight selected pattern */
    }
  </style>
</head>
<body>
  <!-- ✅ Task 1: Main centered layout -->
  <main class="main-wrapper">
    <!-- ✅ Header with student info -->
    <header>
      <h1>Profile Creator</h1>
      <p><strong>Student Full Name</strong><br>Student ID: W2142567<br>The course you study</p>
    </header>

    <!-- ✅ Profile form section -->
    <form class="profile-form">
      <fieldset id="formFieldset">
        <legend>User Details</legend>

        <!-- ✅ Preset name -->
        <label>User Name:
          <input type="text" id="username" value="Oliver Brown" />
        </label>

        <!-- ✅ Age input and feedback -->
        <label>Age:
          <input type="number" id="ageInput" placeholder="Enter an age above 10" />
        </label>
        <div id="ageFeedback">Eligibility message will appear here</div>

        <!-- ✅ Study type -->
        <label>Study Status:
          <select id="studyType">
            <option value="FT UG student">FT UG student</option>
            <option value="PT PG student">PT PG student</option>
          </select>
        </label>

        <!-- ✅ Subscription choices -->
        <label><input type="radio" name="membership" value="annual" /> Standard £5.99 per month - Annual membership apply 20% Discount</label>
        <label><input type="radio" name="membership" value="monthly" checked /> Without Discount</label>

        <!-- ✅ Submit Button -->
        <button type="button" id="submitBtn">Submit Profile</button>
      </fieldset>
    </form>

    <!-- ✅ Profile Result Card -->
    <section class="result-profile">
      <h2>Your Profile</h2>
      <p><strong id="resName">[Your Name]</strong></p>
      <p>Study: <span id="resStudy">[Study Status]</span></p>
      <p>Subscription: <span id="resSub">[Your Subscription Choice]</span></p>
    </section>

    <!-- ✅ Bonus: Background Pattern Selection -->
    <section class="customizer">
      <p>Change the Background Pattern</p>
      <div class="thumbs">
        <div class="thumb" id="thumb1" style="background-image: url('images/pattern1.jpg');"></div>
        <div class="thumb" id="thumb2" style="background-image: url('images/pattern2.jpg');"></div>
        <div class="thumb" id="thumb3" style="background-image: url('images/pattern3.jpg');"></div>
      </div>
    </section>
  </main>

  <!-- ✅ Task 3: JavaScript logic -->
  <script>
    const username = document.getElementById("username");
    const ageInput = document.getElementById("ageInput");
    const studyType = document.getElementById("studyType");
    const membershipRadios = document.getElementsByName("membership");
    const feedback = document.getElementById("ageFeedback");

    const resName = document.getElementById("resName");
    const resStudy = document.getElementById("resStudy");
    const resSub = document.getElementById("resSub");

    const submitBtn = document.getElementById("submitBtn");
    const formFieldset = document.getElementById("formFieldset");

    let selectedMembership = "monthly";

    // ✅ Task 3.1: Live feedback on age eligibility
    function validateEligibility() {
      const age = parseInt(ageInput.value);

      membershipRadios.forEach(radio => {
        if (radio.checked) selectedMembership = radio.value;
      });

      if (selectedMembership === "annual") {
        if (!isNaN(age)) {
          if (age >= 18) {
            feedback.textContent = "✔ You are eligible for discount";
            feedback.style.color = "green";
            feedback.style.borderColor = "green";
          } else {
            feedback.textContent = "✘ You are not eligible for discount";
            feedback.style.color = "red";
            feedback.style.borderColor = "red";
          }
        } else {
          feedback.textContent = "Please enter a valid age";
          feedback.style.color = "orange";
          feedback.style.borderColor = "orange";
        }
      } else {
        feedback.textContent = "Standard subscription selected";
        feedback.style.color = "orange";
        feedback.style.borderColor = "orange";
      }
    }

    // ✅ Task 3.2: Trigger feedback on age or subscription change
    ageInput.addEventListener("input", validateEligibility);
    membershipRadios.forEach(r => r.addEventListener("change", validateEligibility));

    // ✅ Task 3.3: Submit and display the profile
    submitBtn.addEventListener("click", () => {
      const name = username.value;
      const age = parseInt(ageInput.value);
      const study = studyType.value;

      let plan = "Standard £5.99 per month";

      membershipRadios.forEach(r => {
        if (r.checked && r.value === "annual") {
          if (!isNaN(age) && age >= 18) {
            plan = "Standard £" + (5.99 * 0.8).toFixed(2) + " per month (after 20% discount)";
          } else {
            plan = "Standard £5.99 per month (no discount)";
          }
        }
      });

      resName.textContent = name;
      resStudy.textContent = study;
      resSub.textContent = plan;
    });

    // ✅ Bonus Task: Background selector thumbnails
    const thumb1 = document.getElementById("thumb1");
    const thumb2 = document.getElementById("thumb2");
    const thumb3 = document.getElementById("thumb3");

    // Helper to remove 'selected' class from all
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
  </script>
</body>
</html>
```
