```html
<script>
  // 🔗 Select input fields and display elements

  const username = document.getElementById("username"); 
  // <input type="text" id="username" value="Oliver Brown" />

  const ageInput = document.getElementById("ageInput"); 
  // <input type="number" id="ageInput" placeholder="Enter an age above 10" />

  const studyStatus = document.getElementById("studyStatus"); 
  // <input type="text" id="studyStatus" value="FT UG student" />

  const subscriptionType = document.getElementById("subscriptionType"); 
  // <select id="subscriptionType">
  //   <option value="standard">Standard £5.99 per month</option>
  //   <option value="premium">Premium £9.99 per month</option>
  //   <option value="basic">Basic £2.99 per month</option>
  // </select>

  const membershipRadios = document.getElementsByName("membership"); 
  // <input type="radio" name="membership" value="annual" />
  // <input type="radio" name="membership" value="monthly" checked />

  const feedback = document.getElementById("ageFeedback"); 
  // <div id="ageFeedback">Eligibility message will appear here</div>

  // 🔗 Select profile display fields

  const resName = document.getElementById("resName"); 
  // <strong id="resName">[Your Name]</strong>

  const resStudy = document.getElementById("resStudy"); 
  // <span id="resStudy">[Study Status]</span>

  const resSub = document.getElementById("resSub"); 
  // <span id="resSub">[Your Subscription Choice]</span>

  // 🔗 Other key elements

  const submitBtn = document.getElementById("submitBtn"); 
  // <button type="button" id="submitBtn">Submit Profile</button>

  const formFieldset = document.getElementById("formFieldset"); 
  // <fieldset id="formFieldset"> ... background changes apply here ...

  // 🌐 Track which membership is selected
  let selectedMembership = "monthly";

  // ✅ Function to validate age and show discount eligibility
  function validateEligibility() {
    const age = parseInt(ageInput.value);

    // Get the selected membership (monthly or annual)
    membershipRadios.forEach(radio => {
      if (radio.checked) selectedMembership = radio.value;
    });

    // Check if user selected annual plan
    if (selectedMembership === "annual") {
      if (!isNaN(age)) {
        if (age >= 18) {
          // ✅ Eligible for discount
          feedback.textContent = "✔ You are eligible for discount";
          feedback.style.color = "white";
          feedback.style.backgroundColor = "green";
          feedback.style.borderColor = "green";
        } else if (age > 10) {
          // ❌ Not eligible
          feedback.textContent = "✘ You are not eligible for discount";
          feedback.style.color = "white";
          feedback.style.backgroundColor = "red";
          feedback.style.borderColor = "red";
        } else {
          // ⚠️ Age too low
          feedback.textContent = "Please enter an age above 10";
          feedback.style.color = "white";
          feedback.style.backgroundColor = "orange";
          feedback.style.borderColor = "orange";
        }
      } else {
        // ⚠️ Invalid input
        feedback.textContent = "Please enter a valid age";
        feedback.style.color = "white";
        feedback.style.backgroundColor = "orange";
        feedback.style.borderColor = "orange";
      }
    } else {
      // ℹ️ Monthly plan selected, no validation needed
      feedback.textContent = "Standard subscription selected";
      feedback.style.color = "white";
      feedback.style.backgroundColor = "#2196F3";
      feedback.style.borderColor = "#2196F3";
    }
  }

  // 🟡 Event: Validate age and membership in real-time
  ageInput.addEventListener("input", validateEligibility);  // linked to age input
  membershipRadios.forEach(r => r.addEventListener("change", validateEligibility));  // linked to radio buttons

  // 🟢 Event: Handle profile submission
  submitBtn.addEventListener("click", () => {
    const name = username.value;
    const age = parseInt(ageInput.value);
    const study = studyStatus.value;
    const subType = subscriptionType.value;

    let finalSubscription = "";
    let basePrice = 0;

    // Determine base price based on selected plan
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

    // 🧮 Check for annual plan + discount eligibility
    membershipRadios.forEach(r => {
      if (r.checked && r.value === "annual") {
        if (!isNaN(age) && age >= 18) {
          const discountedPrice = (basePrice * 0.8).toFixed(2); // 20% off
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

    // 🖨️ Output to result section
    resName.textContent = name;
    resStudy.textContent = study;
    resSub.textContent = finalSubscription;
  });

  // 🎨 Background selection logic
  const thumb1 = document.getElementById("thumb1"); 
  // <div class="thumb" id="thumb1" style="background-image: url('images/pattern1.jpg');"></div>

  const thumb2 = document.getElementById("thumb2"); 
  // <div class="thumb" id="thumb2" style="background-image: url('images/pattern2.jpg');"></div>

  const thumb3 = document.getElementById("thumb3"); 
  // <div class="thumb" id="thumb3" style="background-image: url('images/pattern3.jpg');"></div>

  // ✨ Helper: Remove selection highlight
  function clearSelection() {
    thumb1.classList.remove("selected");
    thumb2.classList.remove("selected");
    thumb3.classList.remove("selected");
  }

  // 🎯 Event: Apply pattern 1
  thumb1.addEventListener("click", () => {
    clearSelection();
    thumb1.classList.add("selected");
    formFieldset.style.backgroundImage = "url('images/pattern1.jpg')";
    formFieldset.style.backgroundRepeat = "repeat";
    formFieldset.style.backgroundSize = "cover";
  });

  // 🎯 Event: Apply pattern 2
  thumb2.addEventListener("click", () => {
    clearSelection();
    thumb2.classList.add("selected");
    formFieldset.style.backgroundImage = "url('images/pattern2.jpg')";
    formFieldset.style.backgroundRepeat = "repeat";
    formFieldset.style.backgroundSize = "cover";
  });

  // 🎯 Event: Apply pattern 3
  thumb3.addEventListener("click", () => {
    clearSelection();
    thumb3.classList.add("selected");
    formFieldset.style.backgroundImage = "url('images/pattern3.jpg')";
    formFieldset.style.backgroundRepeat = "repeat";
    formFieldset.style.backgroundSize = "cover";
  });

  // 🟢 Run validation once on page load
  validateEligibility();
</script>
```
