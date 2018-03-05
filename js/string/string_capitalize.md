# String capitalize

Задача, сделать заглавной первую букву каждого слова в тексте.

Способы решения:
1. Посимвольный перебор строки
2. Регулярные выражения
3. Через преобразование в массив

## Посимвольный перебор строки

*Через цикл*

```javascript
const capitalizeWords = (str) => {
  let result = '';
  for (let i = 0; i < str.length; i++) {
    const shouldBeBig = str[i] !== ' ' && (i === 0 || str[i - 1] === ' ');
    result += shouldBeBig ? str[i].toUpperCase() : str[i];
  }

  return result;
};
```

*C использованием конечных автоматов*

```javascript
const capitalizeWords = (str) => {
  let result = '';
  let state = 'outside'; // outside, inside

  for (let i = 0; i < str.length; i++) {
    switch (state) {
      case 'inside':
        if (str[i] === ' ') {
          state = 'outside';
        }
        result += str[i];
        break;
      case 'outside':
        if (str[i] !== ' ') {
          result += str[i].toUpperCase();
          state = 'inside';
        } else {
          result += str[i];
        }
        break;
    }
  }

  return result;
};
```

## Через преобразование в массив

```javascript
const capitalizeWords = (string) => {
    const arrayOfWords = string.split(' ');
    const result = arrayOfWords.map((word) => {
            return word[0].toUpperCase() + word.substr(1);
        });
    return result.join(' ');
};
//capitalizeWords('The devil is in the detail') //The Devil Is In The Detail
```

