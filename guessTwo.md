# 🧪 Lab-Based Practical — Student Profile Generator #2

This is a full lab-based practical implementation using just one HTML file. It fulfills the typical marking scheme: HTML structure, CSS styling, JavaScript interaction, and bonus thumbnail-based UI customization.

---

## ✅ Full Source Code (Single HTML with Embedded CSS + JS)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Student Profile Generator</title>
  <style>
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

    .header p {
      font-style: italic;
      margin-bottom: 15px;
    }

    .profile-form label {
      display: block;
      margin-top: 15px;
    }

    #ageFeedback {
      margin: 5px 0 10px;
      color: orange;
      font-weight: bold;
    }

    .result-profile {
      margin-top: 25px;
      padding: 15px;
      border: 1px solid #ccc;
      border-radius: 8px;
      background: #fafafa;
    }

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
      border: 2px solid green;
    }
  </style>
</head>
<body>
  <main class="main-wrapper">
    <header class="header">
      <h1>Student Profile Generator</h1>
      <p><strong>Name:</strong> Amelia Swift<br><strong>ID:</strong> W2157890<br>The course you study</p>
    </header>

    <form class="profile-form">
      <label>User Name:
        <input type="text" id="username" value="Amelia Swift" readonly />
      </label>

      <label>Age:
        <input type="number" id="ageInput" placeholder="Enter your age..." />
      </label>
      <div id="ageFeedback">Age-based eligibility feedback appears here</div>

      <label>Study Type:
        <select id="studyType">
          <option value="Full-Time UG">Full-Time UG</option>
          <option value="Part-Time PG">Part-Time PG</option>
        </select>
      </label>

      <fieldset id="membershipOptions">
        <legend>Membership Type</legend>
        <label><input type="radio" name="membership" value="monthly" checked /> Monthly - £4.99</label>
        <label><input type="radio" name="membership" value="annual" /> Annual - 15% Discount</label>
      </fieldset>

      <button type="button" id="submitBtn">Submit Profile</button>
    </form>

    <section class="result-profile">
      <h2>Your Profile</h2>
      <p><strong id="resName">[Name]</strong></p>
      <p>Study Mode: <span id="resStudy">[...]</span></p>
      <p>Subscription: <span id="resSub">[...]</span></p>
    </section>

    <section class="customizer">
      <p>Customize Background Pattern</p>
      <div class="thumbs">
        <div class="thumb" id="thumb1" style="background-color: #ffe4e1;"></div>
        <div class="thumb" id="thumb2" style="background-color: #e6ffe6;"></div>
        <div class="thumb" id="thumb3" style="background-color: #e0ecff;"></div>
      </div>
    </section>
  </main>

  <script>
    const ageInput = document.getElementById("ageInput");
    const feedback = document.getElementById("ageFeedback");
    const submitBtn = document.getElementById("submitBtn");

    const username = document.getElementById("username");
    const studyType = document.getElementById("studyType");
    const membershipRadios = document.getElementsByName("membership");

    const resName = document.getElementById("resName");
    const resStudy = document.getElementById("resStudy");
    const resSub = document.getElementById("resSub");
    const membershipFieldset = document.getElementById("membershipOptions");

    ageInput.addEventListener("input", () => {
      const age = parseInt(ageInput.value);
      if (!isNaN(age)) {
        if (age >= 18) {
          feedback.textContent = "✔ Eligible for membership discount";
          feedback.style.color = "green";
        } else {
          feedback.textContent = "✘ Not eligible for discount";
          feedback.style.color = "red";
        }
      } else {
        feedback.textContent = "Please enter a valid age.";
        feedback.style.color = "orange";
      }
    });

    submitBtn.addEventListener("click", () => {
      const name = username.value;
      const age = parseInt(ageInput.value);
      const study = studyType.value;

      let selectedPlan = "";
      membershipRadios.forEach((radio) => {
        if (radio.checked) {
          if (radio.value === "annual" && age >= 18) {
            selectedPlan = "Annual - £4.99 (15% off)";
          } else if (radio.value === "annual") {
            selectedPlan = "Annual - £4.99 (no discount)";
          } else {
            selectedPlan = "Monthly - £4.99";
          }
        }
      });

      resName.textContent = name;
      resStudy.textContent = study;
      resSub.textContent = selectedPlan;
    });

    // Bonus thumbnail logic
    const thumbs = document.querySelectorAll(".thumb");

    thumbs.forEach((thumb) => {
      thumb.addEventListener("click", () => {
        thumbs.forEach((t) => t.classList.remove("selected"));
        thumb.classList.add("selected");
        membershipFieldset.style.backgroundColor = thumb.style.backgroundColor;
      });
    });
  </script>
</body>
</html>
