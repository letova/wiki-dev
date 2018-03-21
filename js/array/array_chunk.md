# Chunk

*Через forEach*

```javascript
const getChunked = (array, num) => {
    let result = [];
    let chunk = [];
    array.forEach((el) => {
        if (chunk.length === num) {
            result.push(chunk);
            chunk = [];
        }
        chunk.push(el);
    });
    if (chunk.length !== 0) {
        result.push(chunk);
    }
    return result;
};
//getChunked(['a', 'b', 'c', 'd'], 2)  // [['a', 'b'], ['c', 'd']]
```

*Через цикл*

```javascript
const getChunked = (array, num) => {
    let result = [];
    for (let i = 0; i < Math.ceil(array.length / num); i++) {
        result.push(array.slice(i * num, i * num + num));
    }

    return result;
};
```

*Через итерацию*

```javascript
const getChunked = (coll, size) => {
  const iter = (iterColl, acc = []) => {
    if (iterColl.length === 0) {
      return acc;
    }
    return iter(
      iterColl.slice(size),
      [...acc, iterColl.slice(0, size)],
    );
  };

  return iter(coll);
};
```