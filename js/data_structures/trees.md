# Деревья

**Дерево** — это связный ациклический граф.

```[[1, 4], 2, [3, 8]]```

Корень - сам массив,
Все его элементы - дети,
Если ребенок не массив это листовой узел,
Иначе - внутренний узел.

Такая структура имеет ограничение - внутренние узлы не могут хранить данных.

```[ [{1}, [{4}, {2}]] , {2}, [{3}, [{8}, {1}]] ]```

Первый элемент это значение хранящееся в узле,
Второй элемент - массив детей

## Обход в глубину (Depth-first search)

Структура:

```javascript
{ name: '/',
  children: 
    [ 
      { name: 'etc', children: [Object], meta: {}, type: 'directory' },
      { name: 'hosts', meta: {}, type: 'file' } 
    ],
  meta: {},
  type: 'directory' }
```

Функция, приводящая к нижнему регистру все имена файлов

```javascript
const downcaseFileNames = (node) => {
  if (node.type === 'directory') {
    return { ...node, children: node.children.map(downcaseFileNames) };
  }
  return { ...node, name: node.name.toLowerCase() };
};
```

Функция, которая принимает на вход функцию-обработчик и дерево, а возвращает отображенное дерево.

```javascript
const map = (f, node) => {
  const updatedNode = f(node);

  return node.type === 'directory' ?
    { ...updatedNode, children: node.children.map(n => map(f, n)) } : updatedNode;
};
```

Функция, которая принимает на вход предикат и дерево, а возвращает отфильтрованное дерево по предикату. (Пример: отфильтровывает листья)

```javascript
const filter = (f, node) => {
  if (!f(node)) {
    return null;
  }

  const children = node.children.map(n => filter(f, n)).filter(v => v);
  return { ...node, children };
  //map(...) - в зависимости от предиката элементы сводит к null
  //filter(v => v) - отфильтровывает null
};
```

Функция-редьюсер обрабатывающая файловые деревья

```javascript
const reduce = (f, node, acc) => {
  const newAcc = f(acc, node);

  if (node.type === 'file') {
    return newAcc;
  }
  return node.children.reduce((iAcc, n) => reduce(f, n, iAcc), newAcc);
};
```

Функция, которая принимает на вход файловое дерево и подстроку, а возвращает список файлов, имена которых содержат эту подстроку

```javascript
const findFilesByName = (root, substr) => {
  const iter = (n, ancestry, acc) => {
    const newAncestry = path.join(ancestry, n.name); // функция построения путей
    if (n.type === 'file') {
      return n.name.includes(substr) ? [...acc, newAncestry] : acc;
    }
    return n.children.reduce((cAcc, nn) => iter(nn, newAncestry, cAcc), acc);
  };

  return iter(root, '', []);
};
```
Функция, которая принимает на вход директорию, а возвращает список вложенных узлов (директорий и файлов) и место которое они занимают. 

```javascript
const calculatefilesSize = node => reduce((acc, n) => {
  if (n.type === 'directory') {
    return acc;
  }

  return acc + n.meta.size;
}, node, 0);

const du = (node) => {
  const result = node.children.map(n => [n.name, calculatefilesSize(n)]);
  result.sort(([, size1], [, size2]) => size2 - size1); //дестракчеринг
  return result;
};
```