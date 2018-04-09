# Canvas

## Отрисовка матрицы в canvas

Если браузер не поддерживает ```canvas``` отобразится надпись ```Your browser is not supported```

*HTML*
```
<canvas class="canvas">Your browser is not supported</canvas>
```

*JS*
```javascript
const renderMatrix = (canvas, matrix) => {
    const context = canvas.getContext('2d');
    
    matrix.forEach((row, i) => row.forEach((el, j) => {
        const x = (j + 1) * 11;
        const y = (i + 1) * 11;
        
        context.fillStyle = el;
        context.fillRect(x, y, 10, 10);
    }));

};
```

```javascript
const matrix = [['#B3EC6A', '#E4679C', '#B3EC6A'], ['#E4679C', '#B3EC6A', '#E4679C'], ['#B3EC6A', '#E4679C', '#B3EC6A']];

const canvas = document.querySelector('.canvas');
renderMatrix(canvas, matrix);
```

