# awesome-snippets-js
This page covers advanced snippet techniques for javascript. Describes code snippets that can be used.
You can contribute anytime using Pull Request.

- [Validation](https://github.com/hg-pyun/awesome-snippets-js#validation)
- [Data manipulation](https://github.com/hg-pyun/awesome-snippets-js#data-manipulation)
- [Performance Utility](https://github.com/hg-pyun/awesome-snippets-js#performance)

* * *
## Validation
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

#### Escape Linebreak with React
```javascript
import React from 'react';

function replaceLinebreak(text) {
    const lineArray = text.split('\n');
    const lineArrayLength = lineArray.length;
    return lineArray.map((line, index) => {
        return <span key={index}>{line}{index === lineArrayLength - 1? '' : <br/>}</span>;
    });
}
```
#### Escape Regular Expression String
```javascript
function escapeRegExp(string){
    return string.replace(/[.*+?^${}()|[\]\\]/g, '\\$&'); // $&는 일치한 전체 문자열을 의미합니다.
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

#### Get Touch Position
```javascript
// 'e' is touchEvent Object. (touchStart, touchMove, touchEnd)
function getTouchPositionX(e) {
    return e.changedTouches ? e.changedTouches[0].pageX : e.pageX;
}

function getTouchPositionY(e) {
    return e.changedTouches ? e.changedTouches[0].pageY : e.pageY;
}
```

#### Calculate Drag Angle
```javascript
function getAngle(deltaX, deltaY) {
    return Math.atan(deltaY / deltaX) * 180 / Math.PI;
}
```

#### Highlighting String
```javascript
function highlight(message, keyword) {
    return message && escapeHtml(message).replace(new RegExp(escapeRegExp(keyword), ['gi']), '<em>$&</em>');
}
```

## Performance Utility
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
```
```javascript
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

#### Throttle
```javascript
const throttle = (func, limit) => {
  let lastFunc;
  let lastRan;
  return function() {;
    const context = this;
    const args = arguments;
    if (!lastRan) {
      func.apply(context, args);
      lastRan = Date.now();
    } else {
      clearTimeout(lastFunc)
      lastFunc = setTimeout(function() {
        if ((Date.now() - lastRan) >= limit) {
          func.apply(context, args);
          lastRan = Date.now();
        }
      }, limit - (Date.now() - lastRan));
    }
  }
}
```

#### Debounce
```javascript
const debounce = (func, delay) => {
  let inDebounce
  return function() {
    const context = this;
    const args = arguments;
    clearTimeout(inDebounce);
    inDebounce = setTimeout(() => func.apply(context, args), delay);
  }
}
```
