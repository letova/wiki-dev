# Array Intersection

## Пересечение без дублей

```javascript
const getIntersectionWithoutDoubles = (a1, a2) => {
    const f = (acc, val) => {
      if (a2.indexOf(val) === -1 || acc.indexOf(val) !== -1) {
        return acc;
      } 
      return [...acc, val];
    };
    return a1.reduce(f, []);
};
//getIntersectionWithoutDoubles([1, 2, 3, 4, 4], [6, 3, 4]) //[3, 4]
```

*С использованием Set*

```javascript
const getIntersectionWithoutDoubles = (array1, array2) => {
    const filtered = array1.filter(value => array2.includes(value));
    return [...new Set(filtered)];
};
```

## Пересечение отсортированных массивов, сложность O(n+m)

```javascript
const getIntersectionOfSortedArray = (arr1, arr2) => {
    if (arr1.length === 0 || arr2.length === 0) {
        return [];
    }

    let resultArray = [],
          index1 = 0,
          index2 = 0;

    do {
       if (arr1[index1] === arr2[index2]) {
            resultArray.push(arr1[index1]);
            index1++;
            index2++;
       } else {
            (arr1[index1] > arr2[index2]) ? index2++ : index1++;
       }
    } while (index1 < arr1.length && index2 < arr2.length);

    return resultArray; 
};
//getIntersectionOfSortedArray([1,2,3], [2,3,4]); //[2,3]
```

## Пересечение неотсортированных массивов, сложность O(n+m)

```javascript
const getIntersection = (left, right) => {

    let seen = left.reduce((acc, el) => {
        acc[el] = true;
        return acc;
    }, {});
  
    return right.filter(el => {
        if (el in seen) {
            return true;
        }
        return false;
    });
};
//expect(func([1, 5, 4, 2], [8, 91, 5, 1, 3])).toEqual([5, 1]);
//expect(func([1, 5, 3, 2], [7, 12])).toEqual([]);
```