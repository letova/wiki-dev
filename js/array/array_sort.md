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