# Array Unique

```javascript
const unique = (array) => {
    let seen = {};

    return array.filter(el => {
        if (el in seen) {
            return false;
        }

        seen[el] = true;
        return true;
    });
};
//expect(unique([])).toEqual([]);
//expect(unique([5, 7, 4, 2, 3, 4, 4])).toEqual([5, 7, 4, 2, 3]);
```