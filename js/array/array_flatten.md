# Array flatten

```javascript
const flatten = (array) => {
    return array.reduce((acc, el) => acc.concat(el), []);
};
//flatten([1, 2, [3, 4], 5]) //[1, 2, 3, 4, 5]
```