# Стек

**Стек** (англ. stack — стопка; читается стэк) — абстрактный тип данных, представляющий собой список элементов, организованных по принципу LIFO (англ. last in — first out, «последним пришёл — первым вышел»).

## Проверка сбалансированности парных символов

```javascript
const checkIfBalanced = (string) => {
    let stack = [];
    
    for (let i = 0; i < string.length; i++) {
        const current = string[i];
        if (current === '(') {
            stack.push(current);
        } else if (current === ')') {
            if (stack.length === 0) {
                return false;
            }
            stack.pop();
        }
    }

    return stack.length === 0;
};
//checkIfBalanced('(5 + 6) * (7 + 8)/(4 + 3)') //true
//checkIfBalanced('(4 + 3))') //false
```

Усложненный вариант

```javascript
const checkIfBalanced = (string) => {
    let stack = [];
    const startSymbols = ['{', '(', '<', '['],
        finishSymbols = ['}', ')', '>', ']'], 
        pairs = ['{}', '()', '<>', '[]'];

    for (let i = 0; i < string.length; i++) {
        const current = string[i]; 
        if (startSymbols.includes(current)) {
            stack.push(current);
        } else {
            const previous = stack.pop(); 
            const pair = `${previous}${current}`;
            if (!pairs.includes(pair)) {
                return false;
            }
        };
    }

    return stack.length === 0;
};
//checkIfBalanced('[]{<>}') //true
//checkIfBalanced('[]{(<>}') //false
```

