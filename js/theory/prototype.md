# Прототипы 

Большинство объектов в JS имеют, другой, связанный с ним объект - прототип. Все свойства прототипа доступны в дочернем объекте (prototypal inheritance).

```[[prototype]]``` или ```__proto__``` - ссылка одного объекта на другой;
```prototype``` - указывает какой использовать прототип при создании объекта. Доступно только у функции.
```Animal.prototype = x``` - означает, что все объекты класса Animal будут иметь прототип x (объект).

## Object.create

Запись в прототип

```javascript
const Cat = {
    legs: 4,
    tail: true,
    greet: () => "Maaay!"
};

Object.create(Cat); 
//__proto__: Object ===> 
//legs: 4, tail: true, greet: () => "Maaay!", __proto__: Object

Object.create(null)); 
//no properties
```

Конструктор

```javascript
const Cat = {
    legs: 4,
    tail: true,
    constructor: function(name, color) {
        this.name = name;
        this.color = color;
        return this;
    },
    greet: () => 'Maaay!'
};

Object.create(Cat);
//__proto__: Object ===>
//constructor:ƒ (name, color), greet:() => "Maaay!", legs:4, tail:true, __proto__:Object

Object.create(Cat).constructor('vasya', 'grey');
//color: "gray", name: "vasya", __proto__: Object ===>
//constructor:ƒ (name, color), greet:() => "Maaay!", legs:4, tail:true, __proto__:Object
```

Дочерние классы

```javascript
const Cat = {
    legs: 4,
    tail: true,
    constructor: function(name, color) {
        this.name = name;
        this.color = color;
        return this;
    },
    greet: () => 'Maaay!'
};

const DomesticCat = Object.create(Cat);
DomesticCat.constructor = function(name, color, collar) {
    Cat.constructor.apply(this, [name, color]);
    this.collar = collar;
    return this;
};

Object.create(DomesticCat).constructor('vasya', 'grey', 'false');
//collar:false, color: "gray", name: "vasya", __proto__: Object ===>
//constructor:ƒ (name, color, collar), __proto__:Object ===>
//constructor:ƒ (name, color), greet:() => "Maaay!", legs:4, tail:true, __proto__:Object
```

Методы

```javascript
Cat.isPrototypeOf(cat); //true
```

## New

Конструктор

```javascript
const Cat = function(name, color) {
    this.name = name;
    this.color = color;
};

new Cat('vasya', 'grey');
//color:"grey", name:"vasya", __proto__:Object ===>
//constructor:ƒ (name, color), __proto__:Object
```

Запись в прототип

```javascript
const Cat = function(name, color) {
    this.name = name;
    this.color = color;
};

Cat.prototype.sleep = function() {
    console.log('Sleep...');
};

new Cat('vasya', 'grey');
//color:"grey", name:"vasya", __proto__:Object ===>
//sleep:ƒ (), constructor:ƒ (name, color), __proto__:Object
```

Дочерние классы

```javascript
const Cat = function(name, color) {
    this.name = name;
    this.color = color;
};

Cat.prototype.sleep = function() {
    console.log('Sleep...');
};

DomesticCat = function(name, color, collar) {
    Cat.apply(this, [name, color]);
    this.collar = collar;
};

Object.create(Cat.prototype);
//__proto__:Object ===>
//sleep:ƒ (), constructor: ƒ (name, color), __proto__: Object 
DomesticCat.prototype = Object.create(Cat.prototype);
//DomesticCat.prototype.constructor ==> ƒ (name, color) 
DomesticCat.prototype.constructor = DomesticCat;
//DomesticCat.prototype.constructor ==> ƒ (name, color, collar)

new DomesticCat('tema', 'black', true);
//collar:true, color:"black", name:"tema", __proto__:Object ===>
//constructor:ƒ (name, color, collar), __proto__: Object ===>
//sleep:ƒ (), constructor:ƒ (name, color), __proto__: Object
```

Методы

```javascript
cat instanceof Cat //true
Cat.prototype.isPrototypeOf(cat) //true
```

