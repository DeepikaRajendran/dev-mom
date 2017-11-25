In the [previous post](https://deepikarajendran.github.io/dev-mom/template-data-binding/), we have learnt to do simple template binding from the component property.

### Now, we'll see how to bind property from a component to its parent component .

#### Generate a new component using CLI
```
ng generate component toys
```
The CLI creates new folder `src/app/toys` with files

```
toys.component.ts

toys.component.html

toys.component.css
```

The ToysComponent file is as follows
```Typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-toys',
  templateUrl: './toys.component.html',
  styleUrls: ['./toys.component.css']
})
export class ToysComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

}
```
`ngOnInit` is a [lifecycle hook](https://angular.io/guide/lifecycle-hooks#oninit) method where we can perform our initializations.

#### Add toy property to `src/app/toys/toys.component.ts`
```typescript
export class ToysComponent implements OnInit {
  toy = 'Teddy Bear';
  constructor() { }

  ngOnInit() {
  }

}
```
#### `src/app/toys/toys.component.html`
Add toy component property to the template for binding the value
```html
{{toy}}
```
#### `src/app/app.component.html`
Now , add the `<app-toys>` element to template file, since we have declared `toysComponent` selector as `app-toys` in compoenent file.
```html
  <h1>
    {{title}}!
  </h1>
  <app-toys></app-toys>
  ```

Here is the Output:

![alt-text](https://github.com/DeepikaRajendran/dev-mom/raw/master/images/baby_favorite_toy.png)

It shows both the `title` from the `appComponent` and favorite `toy` from the `toyComponent`.

### Create a Toy Class
Use angular-cli to generate a class
```
ng generate class toy
```
A toy class is created under  `src/app` folder and looks as follows:
```typescript
export class Toy {
}
```
Now, add few properties to the `Toy` class
```typescript
export class Toy {
    name: string,
    color: string
}
```
Import the Toy class in `ToyComponent` as follows:

```typescript
import { Component, OnInit } from '@angular/core';
import {Toy} from '../toy';

@Component({
  selector: 'app-toys',
  templateUrl: './toys.component.html',
  styleUrls: ['./toys.component.css']
})
export class ToysComponent implements OnInit {
  
  toy: Toy = {
    name: 'Teddy Bear',
    color: 'Brown'
  };

  constructor() { }

  ngOnInit() {
  }

}
```
`toy` property is modified to be of type `Toy` and initialized with name `Teddy Bear` and color as `Brown`.

We should change the `toyComponent` template file to display the property values , since we have modified the `toy` from string to object
#### `src/app/toys/toys.component.html`
```html
<p>
  {{ toy.color}} {{toy.name}} 
</p>
```
Here is the Output

![alt_text](https://github.com/DeepikaRajendran/dev-mom/raw/master/images/baby_favorite_toy_color.png)


