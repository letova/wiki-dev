# Array Reverse

```javascript
const reverseArray = (array) => {
    const size = array.length;
    const maxIndex = Math.floor(size / 2);

    for (let i = 0; i < maxIndex; i++) {
        const mirrorIndex = (size - i) - 1;

        [array[i], array[mirrorIndex]] = [array[mirrorIndex], array[i]];
    }
    
    return array;
};
//expect(reverseArray([1, 2, 3, 4])).toEqual([4, 3, 2, 1]);
```