```js
const thumbs = document.getElementsByClassName('thumb'); // NodeList -> thumb1, thumb2, thumb3

const clearSelection = () => {
  [...thumbs].forEach(t => {
    t.classList.remove('selected');
  });
}

// <img src="pattern1.jpg class="thumb" id= "thumb1" />

const selectedThumb = (event) => {
  const thumb = event.target;
  clearSelection();
  thumb.classList.add('selected');
  const selectedImage = thumb.getAttribute('src');
  fieldset.style.backgroundImage = `url(${selectedImage})`;
  fieldset.style.backgroundRepeat = "repeat";
}

[..thumbs].forEach(t => {
  t.addEventListener("click", selectedThumb);
})


```
