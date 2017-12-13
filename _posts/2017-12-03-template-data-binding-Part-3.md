
In this post, we'll see how to add element to the displayed list using

    1. Template Reference Variable
    2. ngModel


Add below code to `src/app/toys/toys.component.html`

```html
   <input #toy placeholder = "Toy Name" />
   <input #color placeholder = "Toy Color" />
```
Here , we are adding 2 input fields to input `toy name and color`, where `#toy`, `#color` are Template Reference Variables.


```
A template reference variable is a reference to the DOm element within a template.
```
`#` symbol before the variable declares it as reference variable and it references the element of the input field.

We can also declare the reference variable with the prefix `ref-`

```html
    <input ref-toy placeholder = "Toy Name" />
    <input ref-color placeholder = "Toy Color" />
```

`#phone` references the whole phone input element, whereas the `phone.value` contains the user typed value.

This reference variable lets us use the value of the DOM element directly inside the template without the need to pass through the component.

Now, add `click` event handling to add the toy to the list.
```html
    <button (click) = "addToy({name: toy.value, color: color.value})" > Add </button>
```
`(click)` braces surrounded here, represent the event binded to the element in action.

`addToy` refers the component property function , which accepts `Toy` Object as its parameter.
And `toy.value, color.value` are passed as Object's properties with `#toy`, `#color` being the Template reference varaibles of the input elements.

Now, we'll handle the click event in `ToyComponent`

Add `addToy` function to `src/app/toys/toy.component.ts`

```typescript
    addToy(toy: Toy){
        this.toys.push(toy);
    }  
```
Here is the output:

![alt-text](https://github.com/DeepikaRajendran/dev-mom/raw/master/images/add-Toy.png)


### Use `ngModel` instead of Template Reference variable.

```typescript
toy : Toy = new Toy();
```
Initiate `toy` property with `Toy` Object.

In `ToyComponent` html template file, modify the input fields to have `ngModel`.

```html
<input [(ngModel)]="toy.name" placeholder = "Toy Name" />
<input [(ngModel)]="toy.color" placeholder = "Toy Color" />
<button (click) = "addToy()" > Add </button>
```
`[(ngModel)]` represents the two way binding of property. Whenever the value of toy gets changed, it get reflected in component's property value.

```typescript
addToy(){
    this.toys.push(this.toy);
  }
```
Now, if you go thorugh the component class, you can see that we are no more passing any parameter from template to component in `addToy()` method, since `ngModel` do the 2-way binding.


