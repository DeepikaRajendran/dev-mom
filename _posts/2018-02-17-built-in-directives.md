In this post, we are going to see the basic built-in directives that angular offers.

### Built-in directives are the attributes we add to our HTML elements that give us dynamic behavior.

#### NgIf

The `ngIf` directive is used when we want to show/hide an element based on a condition. If the result of the expression that is passed to the directive's condition is failed or evaluate to false, the element will be removed from the DOM.

```html
<div *ngIf="false">
    Text is never shown
</div>
```
```html
<div *ngIf="3 > 1">
    Text is displayed
</div>
```

#### NgSwitch

The `ngSwitch` directive is used in case, where there are multiple conditions to be checked to show elements. We can use multiple `ngIf` directives, but to avoid too much complexity, we are provided with `ngSwitch` directive.


```html
<div [ngSwitch]="toy">
    <div *ngSwitchCase="'Teddy'"> 
        Rakshi's Toy 
    </div>
    <div *ngSwitchCase="'Rapunzel'"> 
        Samyuktha's Toy 
    </div>
    <div *ngSwitchCase="'Mickey'"> 
        Diya's Toy 
    </div>
    <div *ngSwitchDefault> 
        Abandoned Toy
    </div>
</div>
```
 We can also use the same `*ngSwitchCase` for different elements.

 ```html
<div [ngSwitch]="toy">
    <div *ngSwitchCase="'Teddy'"> 
        Rakshi's Toy 
    </div>
    <div *ngSwitchCase="'Rapunzel'"> 
        Samyuktha's Toy 
    </div>
    <div *ngSwitchCase="'Mickey'"> 
        Diya's Toy 
    </div>
    <div *ngSwitchCase="'Rapunzel'"> 
        Alvin's Toy 
    </div>
    <div *ngSwitchDefault> 
        Abandoned Toy
    </div>
</div>
```

#### NgStyle

The `ngStyle` directive can set CSS style properties to DOM Elements.

Below are the ways of using `ngStyle` directive.

```html
<div [style.color]="'red'">
    Uses Red Color text
</div>
```
```html
<div [ngStyle]= "{ color :'red', 'background-color' : 'white'}">
</div>
```

#### NgClass

The `ngClass` directive, set and changes CSS classes for the DOM Element.

Usage of `ngClass` is as follows:

```css
.dash-bordered{
    border: 1.5px dashed grey;
}
```
```html
<div [ngClass]= "{'dash-bordered': true}">
    Bordered div
</div>
<div [ngClass]= "{'dash-bordered': false}">
    Div with no border
</div>
```

To add multiple CSS classes to the HTML Element,

```html
<div [ngClass]="['red', 'round']">
</div>
```
#### NgFor

The `ngFor` directive repeats the DOM element by iterating over the each item of the given array.

`ngFor` directive serves the same purpose as `ngRepeat` in Angular JS.

```typescript
this.countries = ['USA', 'India', 'UK'];
```
```html
<div class="ui list" *ngFor="let item of countries">
    <div class="item">{{ item }}</div>
</div>
```
To use the index of the array element,
```html
<div class="ui list" *ngFor="let item of countries; let num = index">
    <div class="item">{{num +1 }}.{{ item }}</div>
</div>
```

#### NgNonBindable
We use `ngNonBindable` directive when we want tell Angular not to compile or bind a particular section of our page.