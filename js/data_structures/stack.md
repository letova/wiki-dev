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

##  Обратная польская запись

[wikipedia](https://ru.wikipedia.org/wiki/%D0%9E%D0%B1%D1%80%D0%B0%D1%82%D0%BD%D0%B0%D1%8F_%D0%BF%D0%BE%D0%BB%D1%8C%D1%81%D0%BA%D0%B0%D1%8F_%D0%B7%D0%B0%D0%BF%D0%B8%D1%81%D1%8C)

```javascript
const calcInPolishNotation = (array) => {
    let stack = [];
    array.forEach((el) => {
        const operators = new Set(['*', '/', '+', '-']);

        if (operators.has(el)) {
            const [b, a] = [stack.pop(), stack.pop()];

            switch (el) {
                case '*':
                    stack.push(a * b);
                    break;
                case '/':
                    stack.push(a / b);
                    break;
                case '+':
                    stack.push(a + b);
                    break;
                case '-':
                    stack.push(a - b);
                    break;
            }

        } else {
            stack.push(el);
        }
    });

    return stack.pop();
};
//expect(calcInPolishNotation([1, 2, '+', 4, '*', 3, '+'])).toBe(15);
```

