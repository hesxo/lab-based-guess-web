# 🧪 Lab-Based Practical — Profile Creator #1

This is a complete lab practical using **HTML**, **CSS**, and **JavaScript**, designed to simulate a real exam question. It includes a form with live discount feedback, profile display, and UI customization using pattern thumbnails.

---

## ✅ Full Source Code (HTML + CSS + JS in one file)

You can copy the following code into a single HTML file and run it in your browser. It includes all required features.

---

### 📦 `profile-creator-1.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Mock Practical</title>
  <style>
    body {
      font-family: Arial, Helvetica, sans-serif;
      background-color: #f0f0f0;
      padding: 20px;
    }

    .container {
      width: 900px;
      margin: 0 auto;
      background-color: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 2px 2px 10px #ccc;
      overflow: hidden;
    }

    .student-info em {
      font-weight: bold;
      display: block;
      margin-bottom: 10px;
    }

    #discountFeedback {
      color: orange;
      border-bottom: 2px solid orange;
      margin-bottom: 10px;
    }

    .profile-card {
      border: 1px solid #ddd;
      margin-top: 20px;
      padding: 10px;
      border-radius: 5px;
    }

    .pattern-thumb {
      width: 25px;
      height: 25px;
      display: inline-block;
      margin-right: 10px;
      border-radius: 50%;
      border: 2px solid transparent;
      cursor: pointer;
    }

    .pattern-thumb.selected {
      border-color: green;
    }
  </style>
</head>
<body>
  <main class="container">
    <div class="student-info">
      <p>
        <em>
          Student Full Name: Oliver Brown<br />
          Student ID: w2142567<br />
          The course you study
        </em>
      </p>
    </div>

    <form class="input-section">
      <label for="userName">User Name:</label>
      <input type="text" id="userName" value="Oliver Brown" readonly />

      <label for="age">Age:</label>
      <input type="number" id="age" placeholder="Enter an age above 10" />
      <div id="discountFeedback">* Feedback appears here</div>

      <label for="studyStatus">Study Status:</label>
      <select id="studyStatus">
        <option value="FT UG student">FT UG student</option>
        <option value="PT PG student">PT PG student</option>
      </select>

      <fieldset id="subscriptionFieldset">
        <legend>Subscription</legend>
        <label>
          <input type="radio" name="subscription" value="standard" checked />
          Standard £5.99 per month
        </label><br />
        <label>
          <input type="radio" name="subscription" value="annual" />
          Annual membership apply 20% Discount
        </label>
      </fieldset>

      <button type="button" id="submitBtn">Submit Profile</button>
    </form>

    <section class="profile-card">
      <h3>Your Profile</h3>
      <p><strong id="profileName">[Your Name]</strong></p>
      <p>Study: <span id="profileStudy">[Study Status]</span></p>
      <p>Subscription: <span id="profileSub">[Your Subscription Choice]</span></p>
    </section>

    <section class="customization">
      <p>Change the Background Pattern</p>
      <div class="patterns">
        <div class="pattern-thumb" id="pattern1" style="background:#f9f9f9;"></div>
        <div class="pattern-thumb" id="pattern2" style="background:#e0f7fa;"></div>
        <div class="pattern-thumb" id="pattern3" style="background:#fff3e0;"></div>
      </div>
    </section>
  </main>

  <script>
    const ageInput = document.getElementById("age");
    const feedback = document.getElementById("discountFeedback");
    const submitBtn = document.getElementById("submitBtn");
    const subscriptionRadios = document.getElementsByName("subscription");

    const profileName = document.getElementById("profileName");
    const profileStudy = document.getElementById("profileStudy");
    const profileSub = document.getElementById("profileSub");
    const userName = document.getElementById("userName");
    const studyStatus = document.getElementById("studyStatus");

    const fieldset = document.getElementById("subscriptionFieldset");

    // Live discount eligibility check
    ageInput.addEventListener("input", () => {
      const age = parseInt(ageInput.value);
      if (!isNaN(age)) {
        if (age >= 18) {
          feedback.textContent = "✔ You are eligible for discount";
          feedback.style.color = "green";
        } else {
          feedback.textContent = "✘ You are not eligible for discount";
          feedback.style.color = "red";
        }
      } else {
        feedback.textContent = "* Feedback appears here";
        feedback.style.color = "orange";
      }
    });

    // On Submit: update profile card
    submitBtn.addEventListener("click", () => {
      const name = userName.value;
      const study = studyStatus.value;
      const age = parseInt(ageInput.value);

      let subscriptionText = "";
      let hasDiscount = false;

      subscriptionRadios.forEach((radio) => {
        if (radio.checked) {
          if (radio.value === "annual") {
            hasDiscount = age >= 18;
            subscriptionText = hasDiscount
              ? "Standard £5.99 per month (after 20% discount)"
              : "Standard £5.99 per month (no discount)";
          } else {
            subscriptionText = "Standard £5.99 per month";
          }
        }
      });

      profileName.textContent = name;
      profileStudy.textContent = study;
      profileSub.textContent = subscriptionText;
    });

    // Pattern selection
    const pattern1 = document.getElementById("pattern1");
    const pattern2 = document.getElementById("pattern2");
    const pattern3 = document.getElementById("pattern3");

    function removePatternSelection() {
      pattern1.classList.remove("selected");
      pattern2.classList.remove("selected");
      pattern3.classList.remove("selected");
    }

    pattern1.addEventListener("click", () => {
      removePatternSelection();
      pattern1.classList.add("selected");
      fieldset.style.backgroundColor = "#f9f9f9";
    });

    pattern2.addEventListener("click", () => {
      removePatternSelection();
      pattern2.classList.add("selected");
      fieldset.style.backgroundColor = "#e0f7fa";
    });

    pattern3.addEventListener("click", () => {
      removePatternSelection();
      pattern3.classList.add("selected");
      fieldset.style.backgroundColor = "#fff3e0";
    });
  </script>
</body>
</html>
