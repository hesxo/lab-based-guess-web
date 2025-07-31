# 🧪 Lab-Based Practical — Profile Creator #3

A complete student lab practical built using **HTML**, **CSS**, and **JavaScript**, with live eligibility feedback, profile display, and background customization thumbnails.

---

## ✅ Full Code (Single HTML File)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Profile Creator</title>
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

    header p {
      font-style: italic;
      margin-bottom: 15px;
    }

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

    .profile-form label {
      display: block;
      margin-top: 15px;
    }

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
    <header>
      <h1>Profile Creator</h1>
      <p><strong>Student Full Name</strong><br>Student ID: W2142567<br>The course you study</p>
    </header>

    <form class="profile-form">
      <fieldset id="formFieldset">
        <legend>User Details</legend>

        <label>User Name:
          <input type="text" id="username" value="Oliver Brown" readonly />
        </label>

        <label>Age:
          <input type="number" id="ageInput" placeholder="Enter an age above 10" />
        </label>
        <div id="ageFeedback">Eligibility message will appear here</div>

        <label>Study Status:
          <select id="studyType">
            <option value="FT UG student">FT UG student</option>
            <option value="PT PG student">PT PG student</option>
          </select>
        </label>

        <label><input type="radio" name="membership" value="annual" /> Standard £5.99 per month - Annual membership apply 20% Discount</label>
        <label><input type="radio" name="membership" value="monthly" checked /> Without Discount</label>

        <button type="button" id="submitBtn">Submit Profile</button>
      </fieldset>
    </form>

    <section class="result-profile">
      <h2>Your Profile</h2>
      <p><strong id="resName">[Your Name]</strong></p>
      <p>Study: <span id="resStudy">[Study Status]</span></p>
      <p>Subscription: <span id="resSub">[Your Subscription Choice]</span></p>
    </section>

    <section class="customizer">
      <p>Change the Background Pattern</p>
      <div class="thumbs">
        <div class="thumb" id="thumb1" style="background-color: #fff9e6;"></div>
        <div class="thumb" id="thumb2" style="background-color: #f0f7ff;"></div>
        <div class="thumb" id="thumb3" style="background-color: #fef0f0;"></div>
      </div>
    </section>
  </main>

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

    ageInput.addEventListener("input", validateEligibility);
    membershipRadios.forEach(r => r.addEventListener("change", validateEligibility));

    submitBtn.addEventListener("click", () => {
      const name = username.value;
      const age = parseInt(ageInput.value);
      const study = studyType.value;

      let plan = "Standard £5.99 per month";

      membershipRadios.forEach(r => {
        if (r.checked) {
          if (r.value === "annual") {
            if (!isNaN(age) && age >= 18) {
              plan = "Standard £5.99 per month (after 20% discount)";
            } else {
              plan = "Standard £5.99 per month (no discount)";
            }
          }
        }
      });

      resName.textContent = name;
      resStudy.textContent = study;
      resSub.textContent = plan;
    });

    // Bonus: background pattern logic
    const thumbs = document.querySelectorAll(".thumb");

    thumbs.forEach((thumb) => {
      thumb.addEventListener("click", () => {
        thumbs.forEach(t => t.classList.remove("selected"));
        thumb.classList.add("selected");
        formFieldset.style.backgroundColor = thumb.style.backgroundColor;
      });
    });
  </script>
</body>
</html>
