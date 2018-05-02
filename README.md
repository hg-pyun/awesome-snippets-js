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
```javascript
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
#### Decimal Math round/floor/ceil
```javascript
// Closure
(function () {
    /**
     * Decimal adjustment of a number.
     *
     * @param {String}  type  The type of adjustment.
     * @param {Number}  value The number.
     * @param {Integer} exp   The exponent (the 10 logarithm of the adjustment base).
     * @returns {Number} The adjusted value.
     */
    function decimalAdjust(type, value, exp) {
        // If the exp is undefined or zero...
        if (typeof exp === 'undefined' || +exp === 0) {
            return Math[type](value);
        }
        value = +value;
        exp = +exp;
        // If the value is not a number or the exp is not an integer...
        if (isNaN(value) || !(typeof exp === 'number' && exp % 1 === 0)) {
            return NaN;
        }
        // Shift
        value = value.toString().split('e');
        value = Math[type](+(value[0] + 'e' + (value[1] ? (+value[1] - exp) : -exp)));
        // Shift back
        value = value.toString().split('e');
        return +(value[0] + 'e' + (value[1] ? (+value[1] + exp) : exp));
    }

    // Decimal round
    if (!Math.round10) {
        Math.round10 = function (value, exp) {
            return decimalAdjust('round', value, exp);
        };
    }
    // Decimal floor
    if (!Math.floor10) {
        Math.floor10 = function (value, exp) {
            return decimalAdjust('floor', value, exp);
        };
    }
    // Decimal ceil
    if (!Math.ceil10) {
        Math.ceil10 = function (value, exp) {
            return decimalAdjust('ceil', value, exp);
        };
    }
})();
```
```javascript
// Round
Math.round10(55.55, -1);   // 55.6
Math.round10(55.549, -1);  // 55.5
Math.round10(55, 1);       // 60
Math.round10(54.9, 1);     // 50
Math.round10(-55.55, -1);  // -55.5
Math.round10(-55.551, -1); // -55.6
Math.round10(-55, 1);      // -50
Math.round10(-55.1, 1);    // -60
// Floor
Math.floor10(55.59, -1);   // 55.5
Math.floor10(59, 1);       // 50
Math.floor10(-55.51, -1);  // -55.6
Math.floor10(-51, 1);      // -60
// Ceil
Math.ceil10(55.51, -1);    // 55.6
Math.ceil10(51, 1);        // 60
Math.ceil10(-55.59, -1);   // -55.5
Math.ceil10(-59, 1);       // -50
```

#### Ellipse String
```javascript
function ellipseStr(str, length) {
    if(!str || !length || str.length <= length){
        return str;
    }

    return `${str.slice(0, length - 3)}...`;
}
```

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
```html
<img data-src="img_url">
```
```javascript
let debounceId = null;
window.addEventListener('scroll', handleScrollEvent, false);

function handleScrollEvent() {
    // simple debounce logic.
    if (debounceId) {
        clearTimeout(debounceId);
    }

    debounceId = setTimeout(() => {
        this.lazyLoadImage();
    }, 100); // lazyload time
}

function lazyLoadImage() {
    const imgList = document.getElementsByClassName('loading');
    if (imgList.length === 0) return;

    const viewportTop = window.scrollY;
    const viewportBottom = scrollTop + window.innerHeight;

    Array.from(imgList).forEach((figure) => {
        const imgOffsetTop = figure.offsetTop;
        const imgOffsetButton = figure.offsetTop + figure.clientHeight;

        if (imgOffsetTop <= viewportBottom && imgOffsetButton >= viewportTop) {
            const $elLink = figure.childNodes[0];
            const $elImg = $elLink.childNodes[0];
            const targetSrc = $elImg.getAttribute('data-src');

            const loader = new Image();

            loader.onload = () => {
                // remove figure, 'loading' class.
                $elImg.src = targetSrc;
            };

            loader.onerror = (e) => {
                // handle image error
            };

            loader.src = targetSrc;
        }
    });
}
```

#### Swipe
```javascript
TBD
```

#### Throttle
```javascript
TBD
```

#### Debounce
```javascript
TBD
```