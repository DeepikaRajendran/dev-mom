In this post, we'll see how to fetch the list of toys from remote server using `HTTP request`.

We'll follow the below steps.

1. Create `ToysService`.
2. Do `Http` request to remote server, in `ToysService`.
3. Call `ToysService` in `ToysComponent` to get the data.

## Create Service
Let's create a `Service` file to place the Http call.


>A service file is generally used to make Http calls or to share data between components.
Sometimes we need to access code across different components. Instead of creating and rewriting the same code in each component, we can write service files to share data.


#### Create  `ToysService`

```
ng g s toys --module=app
```
`g` is the shortcut for `generate`

`s` for `service`

`--module=app` tells the CLI to import and add the new service generated to the array of `providers` in the `app.module.ts` file.

```typescript
import { ToysService } from './toys.service';

...
...
@NgModule({
  ...
  providers: [ColorPipe, ToysService]
})
export class AppModule { }
```

`toys.service.ts` file is created and it look like this.

```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class ToysService {

  constructor() { }

}
```
The service imports `Injectable` symbol and annotates the class with `@Injectable` decorator, which implies that the service might have injected dependencies.

## DO `Http` request

`HttpClient` class is used for communicating with a remote server over `Http`

Import `HttpClientModule` symbol and add it in to `imports` array.

`app.module.ts`

```typescript
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  declarations: [
    AppComponent,
    ToysComponent,
    ColorPipe
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [ColorPipe, ToysService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

`toys.service.ts`

Import `Toy` Model class and import `HttpClient` symbol.

Inject `HttpClient` into the constructor in a private property called `http`.

```typescript
import { Injectable, OnInit } from '@angular/core';
import { Toy } from './toy';
import { HttpClient } from '@angular/common/Http';

@Injectable()
export class ToysService {
  constructor(private http: HttpClient) { }
}
```

Use `HTTP get` method to request data via remote server request.
```typescript
getToys(){
    return this.http.get<Toy[]>('http://empty-night-4832.getsandbox.com/toys');    
  }
```
`HttpClient` method returns response data as `Observable`.
To get the typed Object, apply type specifier `<Toy[]>` to wrap the default untyped JSON object. 

Import `Observable` symbol from `rxjs/Observable`.

```typescript
import { Observable } from 'rxjs/Observable';
```

And call `getToys` method in `ngOnInit` method.
```typescript
ngOnInit(){
    this.getToys();
  }
```
Here is the complete code on `toys.service.ts`
```typescript
import { Injectable, OnInit } from '@angular/core';
import { Toy } from './toy';
import { HttpClient } from '@angular/common/Http';
import { Observable } from 'rxjs/Observable';

@Injectable()
export class ToysService {
  
  constructor(private http: HttpClient) { }

  ngOnInit(){
    this.getToys();
  }

  getToys(){
    return this.http.get<Toy[]>('http://empty-night-4832.getsandbox.com/toys');  
  }
}
```
Access the Remote URL in the browser, to see the data

![alt-text](/images/empty-night-json-output.png)


## Call `ToysService` in `ToysComponent`

Inject `ToyService` in ToyComponent.

```typescript
import { ToysService } from '../toys.service';

constructor(private toysService: ToysService) {  }
```
When Angular creates a `ToyComponent`, the Dependency Injection system sets the `toysService` parameter to the singleton instance of `ToysService`.


> In Angular, services are Singleton. It internally implements the Service Locator Pattern. 
This means each service register itself under one container as a single instance. 

Call `getToys()` method on the `toysService` instance of `ToysService`.

```typescript
ngOnInit() {
    this.toysService.getToys().subscribe(data => {
      this.toys = data;
    });  
    
  }
```
`toysService.getToys()` returns an `Observable` because it in turen use the Angular HttpClient.get method to fetch the toys and HttpClient.get() returns an Observable.

Use `subscribe` method to pass the emitted data, to set the `toys` property.

`toys.component.ts`
```typescript
import { Component, OnInit } from '@angular/core';
import { Toy } from '../toy';
import { ToysService } from '../toys.service';

@Component({
  selector: 'app-toys',
  templateUrl: './toys.component.html',
  styleUrls: ['./toys.component.css']
})
export class ToysComponent implements OnInit {

  toy: Toy = new Toy();
  toys: Toy[];

  constructor(private toysService: ToysService) {  }

  ngOnInit() {
    this.toysService.getToys().subscribe(data => {
      this.toys = data;
    });      
  }

}
```
Output looks like this:

![alt-img](/images/services-http-output.png)

The data from the remote server is loaded in to the 2nd card and as we applied `color` [custom pipe](http://www.developer-mom.com/custom-pipes/), the list of toys appear in the color of the toy.

Full Source code available [here](https://github.com/DeepikaRajendran/baby-app/tree/custom-pipe)