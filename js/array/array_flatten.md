# Array flatten

*До первого уровня*

```javascript
const flatten = (array) => {
    return array.reduce((acc, el) => acc.concat(el), []);
};
//flatten([1, 2, [3, 5], [[4, 3], 2]]) //[1, 2, 3, 5, [4, 3], 2]
```

*Любого уровня*

```javascript
const flatten = array => array.reduce((acc, element) =>
  (element instanceof Array ? [...acc, ...flatten(element)] : [...acc, element]), []);
//flatten([1, 2, [3, 5], [[4, 3], 2]]) //[1, 2, 3, 5, 4, 3, 2]
```