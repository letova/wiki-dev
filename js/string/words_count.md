# Words count

Задача, подсчитать количество вхождений каждого слова в предложение. 

```javascript
const getWordsCount = (string) => {
    const arrayOfWords = string.split(' ');
    return arrayOfWords.reduce((acc, el) => {
        return acc.hasOwnProperty(el) ? {...acc, [el]: (acc[el] + 1)} :
        {...acc, [el]: 1};
    }, {});
};
//getWordsCount('cat dog cat eye see cat dog'); // {cat:3, dog:2, eye:1, see:1}
```