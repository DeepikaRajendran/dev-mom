In this post, we'll see how to build Angular app using Material design.

#### Why should we use Angular Material? Can't we use Bootstrap UI?
 We can use either Bootstrap library or Material to build Angular 5 Apps. But we prefer Material design over Bootstrap, since Material library is -

```
  1. easy to use, as it is built using Angular and Typescript, usage will be as simple as using an Angular component. 
  2. provides high quality UI Components for both Mobile and Desktop devices. 
```

Let's get started with Angular Material.

#### Install Angular material
```
npm install --save @angular/material @angular/cdk 
```

#### Install Angular animations
Install @angular/animations, as some Material components are depend on Angular animations module to do advanced transitions.
```
npm install --save @angular/animations

```

Import `BrowserAnimationsModule` in `app.module.ts` file.
```javascript
import {BrowserAnimationsModule} from '@angular/platform-browser/animations';

@NgModule({
  ...
  imports: [BrowserAnimationsModule],
  ...
})
```
#### Support Gestures

Install hammer.js for supporting gestures in Mobile devices.

```
npm install --save hammerjs
```
#### Include a theme

Add one of the supported themes to the `style.css`

```css
@import "~@angular/material/prebuilt-themes/indigo-pink.css";
```
We can see other available themes inside `/node_modules/@angular/material/prebuilt-themes/` folder.

![alt-text](/images/prebuilt-themes.png)

Alternatively, we can include the theme CSS file inside main index.html.

#### Include Material Icons

Add Material Icons font  to support `mat-icon` in `index.html`.
```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```
For more details, check here [Material Icons](https://google.github.io/material-design-icons/)

Now, let's see how to use Material Components inside our app.

Here is the official website of [Angular Material](https://material.angular.io/), where you can see all the components.

#### Add a simple toolbar with a Icon.

Now, We are going to simply add a title to the toolbar.
Import `MatToolbarModule` and `MatIconModule` to the `app.module.ts` file and add it to `imports` array.

```typescript
import { MatIconModule, MatToolbarModule} from '@angular/material';

@NgModule({
  declarations: [
    AppComponent,
    ToysComponent,
    ColorPipe
  ],
  imports: [
    BrowserModule,
    FormsModule,
    BrowserAnimationsModule,    
    MatToolbarModule,    
    MatIconModule
  ],
  providers: [ColorPipe],
  bootstrap: [AppComponent]
})
```
We can get corresponding module to be imported for each component from the official Website.

Go the [Angular Material](https://material.angular.io/) website -> Component-> click on the particular component-> API.

![alt-text](/images/material-component-api.png)

`mat-toolbar` is the selector for the toolbar component.
`mat-icon` for the Material Icons.

Add it to the `app.component.html`

![alt-text](/images/mat-toolbar.png)
 
 
Added some simple CSS to `app.component.css` file to make look better.
```css
.space {
  flex: 1 1 auto;
}
```
 Now, let's add a color to the toolbar.

![alt-text](/images/mat-toolbar-1.png)
 Few more color options are available to add here - ` primary` and `warn`.

Here is how it looks,

 ![alt-text](/images/toolbar.png)

 We add a Text Input and button to a card,  to add further content to the page.

 Import `MatCardModule`,`MatInputModule`, `MatButtonModule` to `app.module.ts`.

 ```typescript
import { MatIconModule, MatToolbarModule, MatCardModule, MatInputModule, MatButtonModule} from '@angular/material';

@NgModule({
  declarations: [
    AppComponent,
    ToysComponent,
    ColorPipe
  ],
  imports: [
    BrowserModule,
    FormsModule,
    BrowserAnimationsModule,    
    MatToolbarModule,    
    MatIconModule,
    MatCardModule, 
    MatInputModule, 
    MatButtonModule
  ],
  providers: [ColorPipe],
  bootstrap: [AppComponent]
})
```

In `app.component.html`

Add a card
```html
<mat-card></mat-card>
```

Add a `form` and `mat-form-field` selector to add form elements inside the card.
```html
<mat-card>
  <form>
    <mat-form-field>
    </mat-form-field>
  </form>
</mat-card>
```
`mat-form-field` is used to wrap several Material components.

Add an Input text field.
```html
<mat-card>
  <form>
    <mat-form-field>
        <input matInput placeholder="Enter baby's Favorite toy" />
    </mat-form-field>
  </form>
</mat-card>
```
`matInput` is a directive that allows native `<input>` and `<textarea>` elements to work with `<mat-form-field>`.

Add a `button` element.

```html
<mat-card>
  <form>
    <mat-form-field>
      <input matInput placeholder="Enter baby's Favorite toy" />
    </mat-form-field>
    <br>
    <button mat-raised-button color="accent"> Add toy</button>
  </form>
</mat-card>
```
`mat-raised-button` is the used to display Material rectangular button with elevation.

We can also add any of the other Button Attributes -
 `mat-button` (no elevation), `mat-icon-button`, `mat-fab` (circular button), `mat-mini-fab`.

 ![alt-text](/images/material-input.png)

 Let's move on to our old example and apply AAngular material to native elements.
 ```html
 <mat-card>
  <form>
    <mat-form-field>
      <input matInput placeholder="Enter baby's Favorite toy" name="toyName" [(ngModel)]="toy.name" />           
    </mat-form-field>
    <mat-form-field>
      <input matInput placeholder="Toy Color" name="toyColor" [(ngModel)]="toy.color" />
    </mat-form-field>
    <br>
    <button mat-raised-button color="accent" (click)="addToy()"> Add toy</button>
  </form>
</mat-card>
<mat-card>
  <mat-list role="list">
    <mat-list-item role="listitem" *ngFor="let toy of toys">
      <div [innerHTML]="toy| color"></div>
    </mat-list-item>
  </mat-list>
</mat-card>
```
 ![alt-text](/images/material-output.png)