In this post, we'll see how to build our own pipes.

To glance through the built-in pipes, visit my previous post [here](http://www.developer-mom.com/pipes/)

In short, pipes are used to transform the certain input to give the desired output.

Pipes are very easy to use. 
To transform the input, we use `|` symbol followed by the pipe name.

To build a custom pipe, create a new file named as {pipename}.pipe.ts 

To make our tutorial interesting, we are going to list each of baby's toy in its own color.

Let's name the pipe as `color`. Create a file named as `color.pipe.ts` or we can use the angular-cli to generate the same.

```
ng generate pipe color
```
Angular CLI imports the pipe in the `app.module.ts` and add it to the `declarations` array.

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule} from '@angular/forms';

import { AppComponent } from './app.component';
import { ToysComponent } from './toys/toys.component';

import { ColorPipe } from './toys/color.pipe';


@NgModule({
  declarations: [
    AppComponent,
    ToysComponent,
    ColorPipe
  ],
  imports: [
    BrowserModule,
    FormsModule
  ],
  providers: [ColorPipe],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Import `Pipe, PipeTransform` libraries.
```typescript
import { Pipe, PipeTransform} from '@angular/core';
import { Toy } from '../toy';
``` 
Add  decorator `@Pipe` with `name` metadata to the class `ColorPipe`, which should implements the `PipeTransform` interface.

```typescript
@Pipe({name : 'color'})
export class ColorPipe implements PipeTransform{}
```

Now, override the `transform` method of the `PipeTransform` Interface, that accepts an input value followed by optional parameters and returns the transformed value.

```typescript
@Pipe({name:'color'})
export class ColorPipe implements PipeTransform{
    constructor(){      
    }
    
    transform(text: string){      
    }
    
}
```
`src/app/toys/toys.component.html` 
```
<ul>
  <li *ngFor="let toy of toys">
    <div [innerHTML]="toy | color"></div> 
  </li> 
</ul>
```
`[innerHTML]` binds the `toy` object to the DOM and sanitizes the unsafe HTML attributes before binding.

Name of the the pipe class `color` is added to the right side of the `|` symbol, where the `toy` object is passed as input value to the `ColorPipe` class.

`src/app/toys/toys.component.ts`
```typescript
transform(toy: Toy){  
    return `<span style="color:${toy.color};font-weight:bold;">${toy.color}  ${toy.name}</span>`;
}
```

Here, we are styling each toy to appear in its own color in the Toys List.

Let's check the output:

![alt-text](https://github.com/DeepikaRajendran/dev-mom/raw/master/images/custom-pipe-0.png)

Eventhough we are adding the styling for the list of toys, they didn't appear.

The following warning is being displayed in the console.

```
WARNING: sanitizing HTML stripped some content (see http://g.co/ng/security#xss).
```
Since we have used the `[innerHTML]` for binding, it automatically sanitizes and strips some HTML content and issued unsafe HTML warning.
In our case, it stripped the CSS styling.
Hence , we should trust the HTML before injecting it.

Use `DOMSanitizer` to trust the HTML.
```typescript
import { DomSanitizer } from '@angular/platform-browser';

constructor(private sanitizer: DomSanitizer){}

return this.sanitizer.bypassSecurityTrustHtml(`<span style="color:${toy.color};font-weight:bold;">${toy.color}  ${toy.name}</span>`);
```

Now, we'll check the output:

![alt-text](https://github.com/DeepikaRajendran/dev-mom/raw/master/images/custom-pipe-1.png)

Each of the toy appear in its own color text.

Sourcecode is available [here](https://github.com/DeepikaRajendran/baby-app/tree/pipes-part-1).