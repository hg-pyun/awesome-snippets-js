# awesome-snippets-js
This page covers advanced snippet techniques for javascript. Describes code snippets that can be used.
You can contribute anytime using Pull Request.

- [Validation](https://github.com/hg-pyun/awesome-snippets-js#validation)
- [Data manipulation](https://github.com/hg-pyun/awesome-snippets-js#data-manipulation)
- [Performance](https://github.com/hg-pyun/awesome-snippets-js#performance)

* * *
## Validation
#### Check Browser
```javascript
TBD
```

#### Check OS
```javascript
TBD
```

#### Check Android
```javascirpt
TBD
```

#### Check iOS
```javascript
function checkiOS() {
    return /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;
}
```

#### EscapeHTML (XSS)
```javascript
var entityMap = {
    '&': '&amp;',
    '<': '&lt;',
    '>': '&gt;',
    '"': '&quot;',
    "'": '&#39;',
    '/': '&#x2F;',
    '`': '&#x60;',
    '=': '&#x3D;'
};

function escapeHtml (string) {
    return String(string).replace(/[&<>"'`=\/]/g, function fromEntityMap (s) {
        return entityMap[s];
    });
}
```

## Data Manipulation
#### Ellipse String
````javascript
function ellipseStr(str, length) {
    if(!str || !length || str.length <= length){
        return str;
    }

    return `${str.slice(0, length - 3)}...`;
}
````

#### Number With Comma
```javascript
function numberWithComma(number) {
    return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
}
```

#### Trim
```javascript
function trim(string) {
    return string.replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, '');
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

#### Swipe
```javascript
TBD
```

#### throttle
```javascript
TBD
```

#### debounce
```javascript
TBD
```