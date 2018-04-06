# Wiki PHP

## Function

### Variable

* `empty(variable)` - проверяет, пуста ли переменная (PHP 4, PHP 5, PHP 7);
 
* `unset(variable)` - удаляет переменную (PHP 4, PHP 5, PHP 7);

### String

* `explode(' ', string)` - разделяет строку, используя указанный разделитель (PHP 4, PHP 5, PHP 7);

* `str_split(string [, symbol_quantity])` - разбивает строку по символам (PHP 5, PHP 7);

* `ucfirst(string)` — преобразует первый символ строки в верхний регистр (PHP 4, PHP 5, PHP 7);

### Array

* `array_keys` - извлекает из ассоциативного массива ключи и создает из них массив (PHP 4, PHP 5, PHP 7)

* `array_values` - извлекает из ассоциативного массива значения и создает из них массив (PHP 4, PHP 5, PHP 7)

* `array_key_exists(key, array)` - проверяет, присутствует ли в массиве указанный ключ или индекс (PHP 4 >= 4.0.7, PHP 5, PHP 7);

* `in_array(value, array)` - проверяет, присутствует ли в массиве значение (PHP 4, PHP 5, PHP 7)

* `sizeof(array)` — подсчитывает количество элементов массива, псевдоним `count()` (PHP 4, PHP 5, PHP 7);

* `implode(' ', array)` - объединяет элементы массива в строку (PHP 4, PHP 5, PHP 7);

* `max(array)` - возвращает наибольшее значение (PHP 4, PHP 5, PHP 7)

* `is_array(variable)` - определяет, является ли переменная массивом (PHP 4, PHP 5, PHP 7)

* `array_merge(array1, array2)` - объединение массивов (PHP 4, PHP 5, PHP 7)

* `array_unique(array)` - удаляет дубли (PHP 4 >= 4.0.1, PHP 5, PHP 7)

* `array_diff(array1, array2)` - расхождение массивов (PHP 4 >= 4.0.1, PHP 5, PHP 7)

* `array_intersect(array1, array2)` - пересечение массивов (PHP 4 >= 4.0.1, PHP 5, PHP 7)

* `array_sum(array)` - вычисляет сумму значений массива (PHP 4 >= 4.0.4, PHP 5, PHP 7)

## Сторонние библиотеки

### Объектные:

* Collect
* Stringify
* Carbon

### Использующие только функции:

* [Funct](https://github.com/phpfunct/funct#firstncollection-n--1)

`Collection\last([1, 2, 3]);` // => 3

`Collection\rest([5, 4, 3, 2, 1]);` // => [4, 3, 2, 1]

`Collection\without([1, 2, 1, 0, 3, 1, 4], 0, 1);` // => [2, 3, 4]

`Collection\flattenAll(['a', ['b', ['c', ['d']]]]);` // => ['a', 'b', 'c', 'd']

`Collection\union([1, 2, 3], [101, 2, 1, 10], [2, 1]);` // => [1, 2, 3, 101, 10]

`Collection\findWhere(array1, array2)` -  просматривает массив и возвращает первое значение, совпадающее по всем парам ключ-значения переданным вторым параметром.

`Strings\camelize('data_rate');` //'dataRate'

`Strings\contains('PHP is one of the best languages!', 'one');` // true

`Strings\endsWith("hello jon", 'jon');` // => true
Проверяет оканчивается ли строчка на подстроку.

`Strings\right('PHP is one of the best languages!', 1)` //= '!'

* Bottomline
 
## Структуры данных 

### Массив - тип данных

`$animals = ['cats', 'dogs', 'birds'];`

Массивы можно сравнивать
```php
[0, 2] > [0, 1] //1
[1, 12] > [0, 16] //1
```

### Ассоциативный массив (так же говорят «словарь») - абстрактный тип данных

Ассоциативные массивы в PHP имеют порядок, что не типично для такого типа массивов. Пары ключ-значение располагаются в том же порядке, в котором они были добавлены. 

`$user = ['name' => 'Vasya', 'married' => true, 'age' => 25];`

## Примеры

Удалить пустые элементы в массиве
`$new_array = array_diff($old_array, array(''));`






