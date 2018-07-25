# Pagination

```javascript
const pagination = (data, page, perPage) => {
    let index = (page - 1) * perPage;
    return data.slice(index, index + perPage);
}
//expect(pagination([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 2, 3)).toEqual([4, 5, 6]);
```