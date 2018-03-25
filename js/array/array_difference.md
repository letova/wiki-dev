# Array Difference

```javascript
const getDifference = (array, ...rest) => {
    const set = new Set(rest);
    return array.filter(value => !set.has(value));
};
//expect(getDifference([1, 2, 3, 4], 3, 4, 5, 6)).toEqual([1, 2]);
```