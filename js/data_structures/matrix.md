# Матрица

**Матрица** - абстрактный тип данных. Представляет собой двумерный массив, каждый элемент которого имеет два индекса: номер строки и номер столбца.

В **квадратной матрице** имеются две диагонали: главная диагональ (идущая из левого верхнего угла в правый нижний угол) и побочная диагональ (идущая из левого нижнего угла в правый верхний угол).

```matrix[m][n]``` - m — количество строк, n — количество столбцов;

```i = j``` - элемент лежит на главной диагонали матрицы;

```i > j``` - элемент ниже главной диагонали;

```i < j``` - элемент выше главной диагонали;

## Транспонированная матрица 

**Транспонированная матрица** — матрица, полученная из исходной матрицы заменой строк на столбцы.

```javascript
const transposeMatrix = (matrix) => {
    const m = matrix.length;
    const n = matrix[0].length;
    let result = [];

    for (let i = 0; i < n; i++) { 
        result[i] = [];

        for (var j = 0; j < m; j++) {

            result[i][j] = matrix[j][i];
        }
    }

    return result;
};
//expect(rotateMatrix([[1, 2, 3], [4, 5, 6], [7, 8, 9]])).toEqual([[1, 4, 7], [2, 5, 8], [3, 6, 9]]);
```

```javascript
const transposeMatrix = matrix => matrix[0].map((col, i) => matrix.map(row => row[i]));
```

## Поворот матрицы на 90 градусов по часовой стрелке

```javascript
const reverseArray = (array) => {
    const size = array.length;
    const maxIndex = Math.floor(size / 2);

    for (let i = 0; i < maxIndex; i++) {
        const mirrorIndex = (size - i) - 1;

        [array[i], array[mirrorIndex]] = [array[mirrorIndex], array[i]];
    }
    
    return array;
};

const rotateMatrix = (matrix) => {
    const reversed = reverseArray(matrix);
    return transposeMatrix(reversed);
};
//expect(rotateMatrix([[1, 2, 3], [4, 5, 6], [7, 8, 9]])).toEqual([[7, 4, 1], [8, 5, 2], [9, 6, 3]]);
```

## Счетчик элементов в матрице

```javascript
const countElementInMatrix = (element, matrix) => {
    return matrix.reduce((acc, row) => {
        acc += row.filter(el => el === element).length;
        return acc;
    }, 0);
};
//expect(countElementInMatrix(3, [[1, 2, 3], [3, 3, 4]])).toBe(3);
```



