# Топологическая сортировка

**Топологическая сортировка** — упорядочивание вершин бесконтурного ориентированного графа согласно частичному порядку, заданному ребрами орграфа на множестве его вершин.

Функция, которая принимает на вход список зависимостей и возвращает их списком (массив) в правильном порядке

```javascript
const sortDeps = (deps) => {
  const add = (acc, node) => {
    const subDeps = deps[node]; //['thread_safe'];
    const subAcc = subDeps ? subDeps.reduce(add, []) : [];
    return { ...acc, ...subAcc, [node]: true };
  };
  const set = Object.keys(deps).reduce(add, []);
  return Object.keys(set);
};

/*
** const deps = {
**   mongo: [],
**   tzinfo: ['thread_safe'],
**   uglifier: ['execjs'],
**   execjs: ['thread_safe', 'json'],
**   redis: [],
** }
*/

//sortDeps(deps) //['mongo', 'thread_safe', 'tzinfo', 'json', 'execjs', 'uglifier', 'redis']
```