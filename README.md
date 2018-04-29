# awesome-snippets-js
This page covers advanced snippet techniques for javascript. Describes code snippets that can be used.
You can contribute anytime using Pull Request.

- [Validation](https://github.com/hg-pyun/awesome-snippets-js#validation)
- [Data manipulation](https://github.com/hg-pyun/awesome-snippets-js#data-manipulation)
- [Performance](https://github.com/hg-pyun/awesome-snippets-js#performance)

* * *
## Validation
#### Check iOS
```javascript
function checkiOS() {
    return /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;
}
```

## Data Manipulation
#### Number With Comma
```javascript
function numberWithComma(number) {
    return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
}
```

#### Save/Load Local Storage Using Object
```javascript
function setLocalStorageItem(key, item) {
    localStorage.setItem(key, JSON.stringify(item));
}

function getLocalStorageItem(key) {
    return JSON.parse(localStorage.getItem(key));
}
```

## Performance
#### Infinite Scroll
```javascript
// window
window.addEventListener('scroll', handleScrollEvent, false);

function handleScrollEvent() {
    if (window.scrollY + window.innerHeight >= document.body.scrollHeight) {
        // do something such as fetch.
        console.log('touch down');
    }
}

// element
const $el = documnet.getElementById('list');
$el.addEventListener('scroll', handleScrollEvent, false);

function handleScrollEvent() {
    if ($el.scrollTop + $el.offsetHeight >= $el.scrollHeight) {
        // do something such as fetch.
        console.log('touch down');
    }
}
```

#### Lazy Loading
```javascript
TBD
```
