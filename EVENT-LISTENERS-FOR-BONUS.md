```js
// For Bonus

const fieldset = document.getElementById('formFieldset');

const thumbs = document.getElementsByClassName('thumb');

const clearSelection = () => {
  [...thumbs].forEach(t => t.classList.remove('selected'));
}

// <div class="thumbs">
//   <img class="thumb" id="thumb1" src="images/pattern1.jpg">
//   <img class="thumb" id="thumb2" src="images/pattern1.jpg">
//   <img class="thumb" id="thumb3" src="images/pattern1.jpg">
// </div>

const selectedThumb = (event) => {
  const selected = event.target;
  clearSelection();
  selected.classList.add('selected');
  const selectedThumbImage = selected.getAttribute('src');
  fieldset.style.backgroundImage = `url('${selectedThumbImage}')`;
  fieldset.style.backgroundSize = "cover";
  fieldset.style.backgroundRepeat = "repeat";
}

[...thumbs].forEach(t => {
  t.addEventListener("click", selectedThumb)
})

```
