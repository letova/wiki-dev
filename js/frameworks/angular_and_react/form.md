# 1. Вывод значений из инпута

## Angular

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

## React

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

# 2. Обработка изменения инпута

## Angular

### Метод change

Срабатывает при потере фокуса

**app.component.html**
```html
<input [(ngModel)]="name" (change)="onInputChange()" placeholder="Your name" />
```

**app.component.ts**
```javascript
<...>
export class AppComponent  {
    name = '';

    onInputChange(){
        console.log(this.name);
    }
}
```

### Метод ngModelChange

Обрабатывает ввод каждого нового символа

**app.component.html**
```html
<input [(ngModel)]="name" (ngModelChange)="onInputChange()" placeholder="Your name" />
```

## React

См. пример 1.


