In this post, we'll see how to bind data from component to template.


Add `title` property  to `src/app/app.component.ts`
```typescript
export class AppComponent {
  title = 'Baby\'s favorites';
}
```
And in `src/app/app.component.html` file, use interpolation {{ }} to display the component property.

```
<h1>
    {{title}}!
</h1>
```
Now the browser gets updated automatically, since the `ng serve' watches for code changes and 

you can see the component property value is binded to the HTML template and displayed like this:

![alt text](https://github.com/DeepikaRajendran/dev-mom/raw/1564362ef8227e7dadcd9da7bbea554f7002eaf7/images/baby_favorite.png "Result")

Now, we'll go through the `src/app/app.component.ts` file
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
}
```
We should import `Component` symbol from Angular core library and annotate component class with `@Component`.

`@Component` specifies three metadata to the component class.

1. `selector` - the component CSS selector
    The selector 'app-root' is added to `index.html` by cli generator.
    ```HTML
    <body>
        <app-root></app-root>
    </body>
    ```
    This is how the value of title property is appearing in the home page.
2. `templateUrl` - location of the component template file

3. `styleUrls` - location of component CSS file

Add the below style to `src/app/app.component.css`
```CSS
h1{
    color: violet;
}
```
You can see the color of the browser output changes instantly.

![alt_text](https://github.com/DeepikaRajendran/dev-mom/raw/master/images/baby_favorite_1.png)

I have added a simple CSS style, just to show the usage of the file.

Sourcecode is available [here](https://github.com/DeepikaRajendran/baby-app/tree/template_binding)



