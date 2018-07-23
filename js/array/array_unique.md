# Array Unique

*Вариант 1*
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

*Вариант 2*
```javascript
const unique = (array) => array.filter((el, index, array) => array.indexOf(el) === index);
//expect(unique([])).toEqual([]);
//expect(unique([5, 7, 4, 2, 3, 4, 4])).toEqual([5, 7, 4, 2, 3]);
```