# Прототипы 

Большинство объектов в JS имеют, другой, связанный с ним объект - прототип. Все свойства прототипа доступны в дочернем объекте (prototypal inheritance).

## Object.create

```javascript
const Cat = {
    legs: 4,
    tail: true,
    greet: () => "Maaay!"
};

console.log(Object.create(Cat)); 
//__proto__: Object ===> 
//legs: 4, tail: true, greet: () => "Maaay!", __proto__: Object

console.log(Object.create(null)); 
//no propetis
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

console.log(Object.create(Cat));
//__proto__: Object ===>
//constructor:ƒ (name, color), greet:() => "Maaay!", legs:4, tail:true, __proto__:Object

const cat = Object.create(Cat).constructor('vasya', 'grey');
console.log(cat);
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

const cat = Object.create(DomesticCat).constructor('vasya', 'grey', 'false');
console.log(cat);
//collar:false, color: "gray", name: "vasya", __proto__: Object ===>
//constructor:ƒ (name, color, collar), __proto__:Object ===>
//constructor:ƒ (name, color), greet:() => "Maaay!", legs:4, tail:true, __proto__:Object

DomesticCat.sleep = function(){
    console.log('Sleep...');
};
```

Методы

```javascript
Cat.isPrototypeOf(cat); //true
```

## New

```javascript
const Cat = function(name, color) {
    this.name = name;
    this.color = color;
};

const cat = new Cat('vasya', 'grey')
console.log(cat);
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

const cat = new Cat('vasya', 'grey')
console.log(cat);
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

DomesticCat.prototype = Object.create(Cat.prototype); //constructor указывает на функцию Cat
DomesticCat.prototype.constructor = DomesticCat; //исправляем утверждение выше
```

Методы

```javascript
cat instanceof Cat //true
Cat.prototype.isPrototypeOf(cat) //true
```

