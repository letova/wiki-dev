# Input component props

## Angular

**app.component.html**
```html
<greeting [greeting]="greeting" [name]="name"></greeting> 
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

**greeting.component.ts**
```javascript
import { Input, Component } from '@angular/core'; // *

@Component({
  selector: 'greeting',
  template: `<h1>{{ greeting }} {{ name }}!</h1>`
})
export class GreetingComponent  { // *
  @Input() name;
  @Input() greeting;
}
```

**app.module.ts**
```javascript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { GreetingComponent } from './greeting.component'; // *

@NgModule({
  imports:      [ BrowserModule, FormsModule ],
  declarations: [ AppComponent, GreetingComponent ], // *
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

class App extends Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

render(
  <App name="Jane" />,
  document.getElementById('root'),
);
```

# Set default component props

## Angular

Coming soon...

## React

**index.html**
```html
<div id="root"></div>
```

**index.js**
```javascript
import React, { Component } from 'react';
import { render } from 'react-dom';

class App extends Component {
  static defaultProps = { // *
    name: 'anybody',
  };

  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

render(
  <App name="Jane" />,
  document.getElementById('root'),
);
```
