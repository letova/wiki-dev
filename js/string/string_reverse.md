# String Reverse

```javascript
const reverseString = (string) => {
    let index = string.length - 1;
    let result = '';

    while (index > -1) {
        result += string[index];
        index--;
    }

    return result;
};
//expect(reverseString('')).toBe('');
//expect(reverseString('abcd')).toBe('dcba');
```