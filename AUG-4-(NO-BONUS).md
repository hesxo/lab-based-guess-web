```js
// inputs
const ageInput = document.getElementById("ageInput");
const membershipRadios = document.getElementsByName("membership");

// outputs
const ageFeedbackOutput = document.getElementById("ageFeedback");

let selectedMembership ="annual";

const validateEligibility = (age) => {
  if(!isNaN(age)) {
    [...memershipRadios].forEach(r =>{
      if (r.checked) selectedMembership = r.value;
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

// input(s)
const usernameInput = document.getElementById('username');
const studyStatusInput = document.getElementById('studyStatus');
const subscriptionTypeInput = document.getElementById('subscriptionType');

// output(s)
const resNameOutput = document.getElementById('resName');
const resStudyOutput = document.getElementById('resStudy');
const resSubOutput = document.getElementById('resSub');

submitButton.addEventListener("click", () => {
  const name = usernameInput.value;
  const studyStatus = studyStatusInput.value;
  
  resNameOutput.textContent = name;
  resStudyOutput.textContent = studyStatus;
  
  let subText = "";
  const subscription = subscriptionTypeInput.value; // not Standard £5.99 per month
  
  if (subscription == "basic") {
    subText = "Basic £2.99 per month";
  } else if (subscription == "standard") {
    subText = "Standard £5.99 per month";
  } else if (subscription == "premium") {
    subText = "Premium £9.99 per month";
  }
  
  [...membershipRadios].forEach(r => {
    if (r.checked && r.value == "annual") {
      subText = subText + " (20% Discount)";
    } else {
      subText = subText + " (No Discount)";
    }
  });
  
  resSubOutput.textContent = subText;
});

// input(s)

const fieldset = document.getElementById('formFieldset');

const thumb1 = document.getElementById('thumb1');
const thumb2 = document.getElementById('thumb2');
const thumb3 = document.getElementById('thumb3');

function clearSelection() {
  thumb1.classList.remove('selected');
  thumb2.classList.remove('selected');
  thumb3.classList.remove('selected');
}

thumb1.addEventListener("click", () => {
  clearSelection();
  thumb1.classList.add('selected');
  fieldset.style.backgroundImage = "url('pattern1.jpg')";
  fieldset.style.backgroundRepeat = "repeat";
});
thumb2.addEventListener("click", () => {
  clearSelection();
  thumb1.classList.add('selected');
  fieldset.style.backgroundImage = "url('pattern2.jpg')";
  fieldset.style.backgroundRepeat = "repeat";
});
thumb3.addEventListener("click", () => {
  clearSelection();
  thumb1.classList.add('selected');
  fieldset.style.backgroundImage = "url('pattern3.jpg')";
  fieldset.style.backgroundRepeat = "repeat";
});
```
