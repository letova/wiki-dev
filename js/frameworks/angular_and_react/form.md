# Input. Вывод значений


## Angular

### 1.1

Template-Driven

**app.component.html**
```html
<h1>{{ greeting }} {{ name }}!</h1>
<input [(ngModel)]="name" placeholder="Your name" />
```

**app.component.ts**
```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ]
})
export class AppComponent  {
  name = '';
  greeting = 'Hello';
}
```

**app.module.ts**
```javascript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';

@NgModule({
  imports:      [ BrowserModule, FormsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```


### 1.2 

Reactive Forms

**app.component.html**
```html
<h1>{{ greeting }} {{ name }}!</h1>
<input [formControl]="input" placeholder="Your name" /> 
```

**app.component.ts**
```javascript
import { Component } from '@angular/core';
import { FormControl } from '@angular/forms'; // *

@Component({
  ...
})
export class AppComponent  {
  name = '';
  greeting = 'Hello';
  input = new FormControl(); // *

  constructor() { // *
    this.input.valueChanges.subscribe(val => this.name = val);
  }
}
```

**app.module.ts**
```javascript
...
import { ReactiveFormsModule } from '@angular/forms'; // *

import { AppComponent } from './app.component';

@NgModule({
  imports:      [ BrowserModule, FormsModule, ReactiveFormsModule ], // *
  ...
})
export class AppModule { }
```


## React

### 1.1

**index.html**
```html
<div id="root"></div>
```

**index.js**
```javascript
import React, { Component } from 'react';
import { render } from 'react-dom';
import './style.css';

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name: '',
      greeting: 'Hello'
    };
  }

  handleChange = (event) => {
    this.setState({ name: event.target.value });
  };

  render() {
    return (
      <div>
        <h1>{this.state.greeting} {this.state.name}!</h1>
        <input onChange={this.handleChange} placeholder="Your name" />
      </div>
    );
  }
}

render(<App />, document.getElementById('root'));
```

# Input. Обработка изменения


## Angular

### 2.1

Метод ```change``` (cрабатывает при потере фокуса)

**app.component.html**
```html
<input [(ngModel)]="name" (change)="onInputChange()" placeholder="Your name" />
```

**app.component.ts**
```javascript
...
export class AppComponent  {
    name = '';

    onInputChange(){
        console.log(this.name);
    }
}
```


### 2.2 

Метод ```ngModelChange``` (обрабатывает ввод каждого нового символа)

**app.component.html**
```html
<input [(ngModel)]="name" (ngModelChange)="onInputChange()" placeholder="Your name" />
```


### 2.3

```Subscribe``` См. пример 1.2 


## React

См. пример 1.1


