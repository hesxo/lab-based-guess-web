```js
// inputs
const usernameInput = document.getElementById("username");
const ageInput = document.getElementById("ageInput");
const studyStatusInput = document.getElementById("studyStatus");
const subscriptionTypeInput = document.getElementById("subscriptionType");
const membershipRadios = document.getElementsByName("membership");

// outputs
const ageFeedbackOutput = document.getElementById("ageFeedback");

let selectedMembership ="annual";

function validateEligibility(age) {
  if(!isNaN(age)) {
    [...memershipRadios].foreach(r =>{
      if(r.checked) selectedMembership = r.value;
    });
    if (selectedMembership == "annual") {
      if(age >= 18) {
        ageFeedbackOutput.textContent = "✔ You are eligible for discount"
        ageFeedbackOutput.style.color = "green";
      } else {
        ageFeedbackOutput.textContent = "✘ You are not eligible for discount";
        ageFeedbackOutput.style.color = "red";
    } else {
      ageFeedbackOutput.textContent = "";
    }
}

// eventListeners => (ageInput, membershipRadios)
// String >>> Integer { parseInt() }
ageInput.addEventListener("input", validateEligibility(parseInt(ageInput.value)));
[...memershipRadios].forEach(r => {
  r.addEventListener("change", validateEligibility(parseInt(ageInput.value)))
});

// button
const submitButton = document.getElementById('submitBtn');

// outputs
const resNameOutput = document.getElementById('resName');
const resStudyOutput = document.getElementById('resStudy');


submitButton.addEventListener("click", () => {
  const name = usernameInput.value;
  const studyStatus = studyStatusInput.value;
  
  resNameOutput.textContent = name;
  resStudyOutput.textContent = studyStatus;
  
  const subscription = subscriptionTypeInput.value; // basic, standard, premium
  
  let subText = "";
  let basePrice = 0;
  
  if (subscription == "basic") {
    subText = "Basic £2.99 per month";
    basePrice = 2.99;
  } else if (subscription == "standard") {
    subText = "Standard £5.99 per month"
    basePrice = 5.99;
  } else if (subscription == "premium") {
    subText = "Premium £9.99 per month"
    basePrice = 9.99;
  }
  
  [...memershipRadios].forEach(r => {
    if (r.checked && r.value == "annual") {
      // 20k apply karana formula eka
      const discount = basePrice * 0.8;
      
      if (subscription == "basic") {
        subText = "Basic £" + discount + " per month";
      } else if (subscription == "standard") {
        subText = "Standard £" + discount + " per month";
      } else if (subscription == "premium") {
        subText = "Premium £" + discount + " per month";
      }
      subText = subText + " (20% Discount)";
    } else {
      subText = subText + " (No Discount)";
    }
  });
  
  const resSubOutput = document.getElementById('resSub');
  resSubOutput.textContent = subText;
});

const thumb1 = document.getElementById('thumb1');
const thumb2 = document.getElementById('thumb2');
const thumb3 = document.getElementById('thumb3');

const fieldset = document.getElementById('formFieldset');

function clearSelection() {
  thumb1.classList.remove('selected');
  thumb2.classList.remove('selected');
  thumb3.classList.remove('selected');
}

thumb1.addEventListener("click", () => {
  clearSelection();
  thumb1.classList.add('selected');
  fieldset.style.backgroundImage = "url('pattern1.jpg')"
  fieldset.style.backgroundRepeat = "repeat";
});
thumb2.addEventListener("click", () => {
  clearSelection();
  thumb2.classList.add('selected');
  fieldset.style.backgroundImage = "url('pattern2.jpg')"
  fieldset.style.backgroundRepeat = "repeat";
});
thumb3.addEventListener("click", () => {
  clearSelection();
  thumb3.classList.add('selected');
  fieldset.style.backgroundImage = "url('pattern3.jpg')"
  fieldset.style.backgroundRepeat = "repeat";
});
```
