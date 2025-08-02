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

const validateEligibility = () => {
    var age = parseInt(ageInput.value);
    
    membershipRadios.forEach(r => {
        if (r.checked) selectedMembership = r.value;
    })
    
    if (!isNaN(age)) {
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
    } else {
        feedbackOutput.textContent = "Please enter a valid age";
    }
}

ageInput.addEventListener("input", validateEligibility);
membershipRadios.forEach(r => {
    r.addEventListener("change", validateEligibility);
});

submitButton.addEventListener("click", () => {
    const name = usernameInput.value;
    const study = studyStatusInput.value;
    const age = parseInt(ageInput.value);
    
    resNameOutput.textContent = name;
    resStudyOutput.textContent = study;
    
    const subscription = subscriptionTypeInput.value;
    
    var subText = "";
    var basePrice = 0;
    
    if (subscription == "basic") {
        subText = "Basic £2.99 per month";
        basePrice = 2.99;
    } else if (subscription == "standard") {
        subText = "Standard £5.99 per month";
        basePrice = 5.99;
    } else if (subscription == "premium") {
        subText = "Premium £9.99 per month";
        basePrice = 9.99;
    }
    
    membershipRadios.forEach(r => {
        if (r.checked && r.value == "annual") {
            if (!isNaN(age) && age >= 18) {
                const discount = basePrice * 0.8;
                if (subscription == "basic") {
                    subText = "Basic £" + basePrice + " per month";
                } else if (subscription == "standard") {
                    subText = "Basic £" + basePrice + " per month";
                } else if (subscription == "premium") {
                    subText = "Basic £" + basePrice + " per month";
                }
            }
            subText = subText + "(20% Discount)";
        } else {
            subText = subText + "(No Discount)";
        }
    });
    
    resSubOutput.textContent = subText;
});

const thumb1 = document.getElementById('thumb1');
const thumb2 = document.getElementById('thumb2');
const thumb3 = document.getElementById('thumb3');

const clearSelection = () => {
    thumb1.classList.remove('selected');
    thumb2.classList.remove('selected');
    thumb2.classList.remove('selected');
}

const fieldImage = document.getElementById('formFieldset');

thumb1.addEventListener("click", () => {
    clearSelection();
    thumb1.classList.add('selected');
    fieldImage.style.backgroundImage = "url('thumb1.jpg')";
    fieldImage.style.backgroundSize = "cover";
    fieldImage.style.backgroundRepeat = "repeat";
});
thumb2.addEventListener("click", () => {
    clearSelection();
    thumb2.classList.add('selected');
    fieldImage.style.backgroundImage = "url('thumb2.jpg')";
    fieldImage.style.backgroundSize = "cover";
    fieldImage.style.backgroundRepeat = "repeat";
});
thumb3.addEventListener("click", () => {
    clearSelection();
    thumb3.classList.add('selected');
    fieldImage.style.backgroundImage = "url('thumb3.jpg')";
    fieldImage.style.backgroundSize = "cover";
    fieldImage.style.backgroundRepeat = "repeat";
});


```
