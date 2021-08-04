# Beautiful Code

## JavaScript/TypeScript

### jQuery-like Selector

```javascript
// Original:
const $ = s => (n => n.length > 1 ? n : n[0])(document.querySelectorAll(s));

// Easier to understand versions:
function $(s) {
    return (function (n) {
        return n.length > 1 ? n : n[0];
    })(document.querySelectorAll(s));
}

const _ = n => n.length > 1 ? n : n[0];
const $ = s => _(document.querySelectorAll(s))

function $(s) {
    return _(document.querySelectorAll(s));

    function _(n) {
        return n.length > 1 ? n : n[0];
    }
}
```
