# Matrix

## Отрисовка матрицы в canvas

Если браузер не поддерживает ```canvas``` отобразится надпись ```Your browser is not supported```

*HTML*
```
<canvas class="canvas">Your browser is not supported</canvas>
```

*JS*
```javascript
const renderMatrix = (canvas, matrix, size, borderSize) => {
    const context = canvas.getContext('2d');
    
    matrix.forEach((row, i) => row.forEach((el, j) => {
        const x = (j + 1) * (size + borderSize);
        const y = (i + 1) * (size + borderSize);
        
        context.fillStyle = el;
        context.fillRect(x, y, size, size);
    }));

};
```

```javascript
const matrix = [['#B3EC6A', '#E4679C', '#B3EC6A'], ['#E4679C', '#B3EC6A', '#E4679C'], ['#B3EC6A', '#E4679C', '#B3EC6A']];

const canvas = document.querySelector('.canvas');
renderMatrix(canvas, matrix, 20, 1);
```

## Создание таблицы из матрицы

*JS*
```javascript
const createTableFromMatrix = (matrix) => {
    const table = document.createElement('table');

    matrix.forEach((row, i) => {
        const rowEl = document.createElement('tr');
        rowEl.setAttribute('data-tr', i);

        row.forEach((el, j) => {
            const cellEl = document.createElement('td');
            cellEl.setAttribute('data-td', j);

            rowEl.appendChild(cellEl);
        })

        table.appendChild(rowEl);
    });

    return table;
};
```
