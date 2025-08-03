```js
// Input
const usernameInput = document.getElementById('username');
const ageInput = document.getElementById('ageInput');
const studyStatusInput = document.getElementById('studyStatus');

const subscriptionTypeInput = document.getElementById('subscriptionType');

const membershipRadios = document.getElementsByName('membership'); // annual, monthly

// Button
const submitButton = document.getElementById('submitBtn');

// Output
const feedbackOutput = document.getElementById('ageFeedback');
const resNameOutput = document.getElementById('resName');
const resStudyOutput = document.getElementById('resStudy');
const resSubOutput = document.getElementById('resSub');

let selectedMembership = "monthly";

const validateEligibility = (age) => {
    if (!isNaN(age)) {
        [...membershipRadios].forEach(r => {
          if (r.checked) selectedMembership = r.value;
        })
        if (selectedMembership == "annual") {
            if (age >= 18) {
                feedbackOutput.textContent = "✔ You are eligible for discount";
                feedbackOutput.style.color = "green";
            } else {
                feedbackOutput.textContent = "✘ You are not eligible for discount";
                feedbackOutput.style.color = "red";
            }
        } else {
            feedbackOutput.textContent = "Standard subscription selected";
            feedbackOutput.style.color = "yellow";
        }
        return true;
    } else {
        feedbackOutput.textContent = "Please enter a valid age";
        return false;
    }
}

ageInput.addEventListener("input", validateEligibility(parseInt(ageInput.value)));
[...membershipRadios].forEach(r => {
  r.addEventListener("change", validateEligibility(parseInt(ageInput.value)));
});

submitButton.addEventListener("click", () => {
  const name = usernameInput.value;
  const study = studyStatusInput.value;
  const subType = subscriptionTypeInput.value;
  
  resNameOutput.textContent = name;
  resSubOutput.textContent = study;
  
  var subText = "";
  
  if (subType == "basic") {
    subText = "Basic £2.99 per month";
  } else if (subType == "standard") {
    subText = "Standard £5.99 per month";
  } else if (subType == "premium") {
    subText = "Premium £9.99 per month";
  }
  
  [...membershipRadios].forEach(r => {
    if (r.checked && r.value == "annual") {
      subText = subText + " (20% Discount)";
    } else {
      subText = subText + " (No Discount)";
    }
  })
  resSubOutput.textContent(subText);
});

const thumb1 = document.getElementById('thumb1');
const thumb2 = document.getElementById('thumb2');
const thumb3 = document.getElementById('thumb3');

function clearSelection() {
  thumb1.classList.remove('selected');
  thumb2.classList.remove('selected');
  thumb3.classList.remove('selected');
}

const fieldset = document.getElementById('formFieldset');

thumb1.addEventListener("click", () => {
  clearSelection();
  thumb1.classList.add('selected');
  fieldset.style.backgroundImage = "url('pattern1.jpg')";
  fieldset.style.backgroundSize = "cover";
  fieldset.style.backgroundRepeat = "repeat";
})

thumb2.addEventListener("click", () => {
  clearSelection();
  thumb2.classList.add('selected');
  fieldset.style.backgroundImage = "url('pattern2.jpg')";
  fieldset.style.backgroundSize = "cover";
  fieldset.style.backgroundRepeat = "repeat";
})

thumb3.addEventListener("click", () => {
  clearSelection();
  thumb3.classList.add('selected');
  fieldset.style.backgroundImage = "url('pattern3.jpg')";
  fieldset.style.backgroundSize = "cover";
  fieldset.style.backgroundRepeat = "repeat";
})
```
