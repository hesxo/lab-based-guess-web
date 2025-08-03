```js
submitButton.addEventListener("click", () => {
  const name = usernameInput.value;
  const study = studyStatusInput.value;
  const subType = subscriptionTypeInput.value;
  
  resNameOutput.textContent = name;
  resSubOutput.textContent = study;
  
  var subText = "";
  var basePrice = 0;
  
  if (subType == "basic") {
    subText = "Basic £2.99 per month";
    basePrice = 2.99;
  } else if (subType == "standard") {
    subText = "Standard £5.99 per month";
    basePrice = 5.99;
  } else if (subType == "premium") {
    subText = "Premium £9.99 per month";
    basePrice = 9.99;
  }
  
  [...membershipRadios].forEach(r => {
    if (r.checked && r.value == "annual") {
      const discount = basePrice * 0.8
      if (subType == "basic") {
        subText = "Basic £" + discount " per month";
      } else if (subType == "standard") {
        subText = "Standard £" + discount " per month";
      } else if (subType == "premium") {
        subText = "Premium £" + discount " per month";
      }
      subText = subText + " (after 20% discount)"
    } else {
      subText = subText + " (No Discount)";
    }
  })
  resSubOutput.textContent(subText);
});
```
