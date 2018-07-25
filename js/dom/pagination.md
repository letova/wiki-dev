# Pagination

```javascript
const getDataForSelectedPage = (data, page, perPage) => {
    let index = (page - 1) * perPage;
    return data.slice(index, index + perPage);
};
//expect(getDataForSelectedPage([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 2, 3)).toEqual([4, 5, 6]);
```

```javascript
const getPageNumbers = (data, perPage) => {
    return Array(Math.ceil(data.length / perPage)).fill(0).map((x, i) => i + 1);
};
//expect(getPageNumbers([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 3)).toEqual([1, 2, 3, 4]);
```