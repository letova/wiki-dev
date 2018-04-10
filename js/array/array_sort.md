# Array Sort

## Bubble Sort

```javascript
const bubbleSort = (array) => {
    let size = array.length,
        swapped;
    do {
        swapped = false;
        for (let i = 0; i < size - 1; i++) {
            if (array[i] > array[i + 1]) {
                
                [array[i], array[i + 1]] = [array[i + 1], array[i]];
                swapped = true;
            }
        }
        size--;
    } while (swapped);

    return array;
};
//expect(bubbleSort([3, 2, 10, -2, 0])).toEqual([-2, 0, 2, 3, 10]);
```

## Check Sort

```javascript
const isSorted = (array) => {
    for (let i = 0; i < array.length; i++) {
        let current = array[i];
        let next = array[i + 1];

        if (next && current > next) {
            return false;
        }
    }
    return true;
};
//expect(isSorted([])).toBe(true);
//expect(isSorted([1, 7, -4, 8, 12])).toBe(false);
//expect(isSorted([-Infinity, -3, 0, 2, 15])).toBe(true);
```