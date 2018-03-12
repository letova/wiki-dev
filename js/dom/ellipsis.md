# Ellipsis

Обрезает текст у каждого элемента dom-коллекции ```(collection)``` по указанное количество символов ```(size)```.

```javascript
const ellipsis = (collection, size) => {
    return [].map.call(collection, ((el) => {
        el.innerText = el.innerText.slice(0, size) + ' ...';
        return el;
    }));
};
```