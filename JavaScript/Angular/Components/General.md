# Components

A component consists of:

* An HTML template that declares what renders on the page. Ex: `app.component.html`
* A Typescript class that defines behavior. Ex: `app.component.ts`
* A CSS selector that defines how the component is used in a template. Ex: `app.component.css`
* Optionally, CSS styles applied to the template

## Creating Components

### Automatically using Angular CLI

```bash
ng generate ./component
```

### Manually

1. Create a new file called `<component-name>.components.ts` 

2. Import Component

   ```javascript
   import { Component } from '@angular/core';
   ```

3. Add component decorator

   ```javascript
   @Component({
   })
   ```

4. Add selector, template, and style references

   ```javascript
   @Component({
     selector: 'app-component-overview',
     templateUrl: './component-overview.component.html',
     styleUrls: ['./component-overview.component.css']
   })
   ```

5. Export the `class` for the component

   ```js
   export class ComponentOverviewComponent {
   
   }
   ```

### Example

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-item',
  templateUrl: './item.component.html',
  styleUrls: ['./item.component.css']
})

export class ItemComponent {
// your code goes here
}
```

### Declaring Selector

The selector represents the name of the component tag in the html code. It represents where the html code of the component will be placed.

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-item',
  templateUrl: './item.component.html',
  styleUrls: ['./item.component.css']
})
```

```html
<p>
    <app-item></app-item>
</p>
```

### Declaring Templates

#### From File

```js
@Component({
  selector: 'app-component-overview',
  templateUrl: './component-overview.component.html',
})
```

#### Inline

```js
// Use ' for single line and ` for multiple lines
@Component({
  selector: 'app-component-overview',
  template: `
    <h1>Hello World!</h1>
    <p>This template definition spans multiple lines.</p>
  `
})
```

### Declaring Styles

#### From File

```js
@Component({
  selector: 'app-component-overview',
  templateUrl: './component-overview.component.html',
  styleUrls: ['./component-overview.component.css']
})
```

#### Inline

Uses an array of strings that contains the CSS rule declarations.

```js
@Component({
  selector: 'app-component-overview',
  template: '<h1>Hello World!</h1>',
  styles: ['h1 { font-weight: normal; }']
})
```

## Declaring Classes

### Using Class Variables in HTML

Use `{{ code }}` in the html code

```tsx
export class ItemComponent {
    test : string = 'test'
}
```

```html
<p> {{ test }} </p>
```

### Class Constructor and `ngOnInit()`

```tsx
export class ItemComponent implements OnInit {
    constructor() {}
    ngOnInit() : void {}
}
```

### Passing Variables into Components

```tsx
export class TextComponent {
    @Input() text : string;
    @Input() size : int;
}
```

```html
<header>
	<app-TextComponent [text]="This is text" [size]=16></app-TextComponent>
</header>
```

## Directives

The 3 types of directives are:

1. **Components:** Directives with a template
2. **Attribute Directives:** Change the appearance or behavior of an element, component, or another directive
3. **Structural Directives:** Change the DOM layout by adding or removing DOM elements

### Built-in Attribute Directives

#### NgClass

Adds and removes a set of CSS classes

##### Using NgClass with an expression

Say that `app.component.ts` has an `isSpecial` variable that is set to true. The below code applies the class `special` to the `div` as `isSpecial` is `true`

```html
<!-- toggle the "special" class on/off with a property -->
<div class="special" [ngClass]="isSpecial ? 'special' : ''">This div is special</div>
```

##### Using NgClass with a method

In the component class, have an object that adds or removes classes based on the state of other component properties.

```js
currentClasses: Record<string, boolean> = {};
/* . . . */
setCurrentClasses() {
  // CSS classes: added/removed per current state of component properties
  this.currentClasses =  {
    saveable: this.canSave,
    modified: !this.isUnchanged,
    special:  this.isSpecial
  };
}
```

Then, in the template:

```html
<div [ngClass]="currentClasses">This div is initially saveable, unchanged, and special.</div>
```

#### NgStyle

NgStyle can be used to set multiple inline styles simultaneously

In the component class:

```typescript
currentStyles: Record<string, string> = {};
/* . . . */
setCurrentStyles() {
  // CSS styles: set per current state of component properties
  this.currentStyles = {
    'font-style':  this.canSave      ? 'italic' : 'normal',
    'font-weight': !this.isUnchanged ? 'bold'   : 'normal',
    'font-size':   this.isSpecial    ? '24px'   : '12px'
  };
}
```

In the template class:

```html
<div [ngStyle]="currentStyles">
  This div is initially italic, normal weight, and extra large (24px).
</div>
```

#### NgModel

NgModel can be used to display and update data properties when the user makes changes. It binds the value of HTML controls like `input`, `select`, and `textarea` to app data.

##### Example with FormsModule

First, import `FormsModule` by adding it to the NgModule's imports list in `app.module.ts`

```tsx
import { FormsModule } from '@angular/forms'; // <--- JavaScript import from Angular
/* . . . */
@NgModule({
  /* . . . */

  imports: [
    BrowserModule,
    FormsModule // <--- import into the NgModule
  ],
  /* . . . */
})
export class AppModule { }
```

 Then, add the NgModel binding to an HTML `<form>` element:

```html
<label for="example-ngModel">[(ngModel)]:</label>
<input [(ngModel)]="currentItem.name" id="example-ngModel">
```

You can have custom configuration with an expanded form of NgModel:

```html
<input [ngModel]="currentItem.name" (ngModelChange)="setUppercaseName($event)" id="example-uppercase">
```

The result is as follow:

![NgModel variations](https://angular.io/generated/images/guide/built-in-directives/ng-model-anim.gif)

##### Form Example

```tsx
import {Component} from '@angular/core';

@Component({
  selector: 'example-app',
  template: `
    <input [(ngModel)]="name" #ctrl="ngModel" required>

    <p>Value: {{ name }}</p>
    <p>Valid: {{ ctrl.valid }}</p>

    <button (click)="setValue()">Set value</button>
  `,
})
export class SimpleNgModelComp {
  name: string = '';

  setValue() {
    this.name = 'Nancy';
  }
}
```

## Events

To assign an event, just put parenthesis with the event type

```html
<button (click)="onClick"></button>
```

### Custom Function

To make it so each instance of the component can execute a custom function, you have to output an EventEmitter

```tsx
export class ButtomComponent {
    @Input() text : string;
    @Input() color : string;
    @Output() btnClick = new EventEmitter
    onClick() {
        this.btnClick.emit();
    }
}
```

### Button Example

In `button.component.ts`:

```tsx
export class ButtomComponent {
    @Input() text : string;
    @Input() color : string;
    @Output() btnClick = new EventEmitter
    isClicked : boolean = false;
    onClick() {
        this.isClicked = true;
        this.btnClick.emit();
    }
}
```

In `button.component.html`:

```html
<button [ngClass]="isClicked ? 'isClicked' : ''" (click)="onClick"
        [ngStyle]="{ 'background-color': color }">
    {{ text }}
</button>
```

In `button.component.css`:

```css
.isClicked {
    color: grey;
}
```

In `app.component.ts`:

```tsx
export class app {
	printHi() {
        console.log("Hi");
    }    
}
```

In `app.component.html`:

```html
<app-button [text]="Click Me!" [color]="red" (btnClick)="printHi"></app-button>
```

### Built-in Structural Directives

#### NgIf

Add or remove an element by applying an `NgIf` directive to a host element. If `NgIf` is `false`, then the element and its decedents are removed from the DOM. 

##### Example

```html
<app-item-detail *ngIf="isActive" [item]="item"></app-item-detail>
```

##### Example with Null value

If the element assigned to `NgIf` is null, then Angular won't attempt to display the element, which can protect against null variables. In the following example, `currentCustomer` is null.

```html
<div *ngIf="currentCustomer"> Hello, {{currentCustomer.name}} </div>
```

#### NgFor

`NgFor` is used to display a list of items.

##### Listing Items

```html
<div *ngFor="let item of items">{{item.name}}</div>
```

The string `"let item of items"` tells Angular to do the following:

* Store each item in the items array in the local `item` looping variable
* Make each item available to the templated HTML for each iteration
* Translate `"let item of items"` into an <ng-template> around the host element
* Repeat the <ng-template> for each `item` in the list

##### Repeating a Component View

Apply the `NgFor` to the selector

```html
<app-item-detail *ngFor="let item of items" [item]="item"></app-item-detail>
```

##### Getting the Index of NgFor

```html
<div *ngFor="let item of items; let i=index">{{i + 1}} - {{item.name}}</div>
```

##### Repeating Elements when a Condition is True

Put the `NgIf` on a container that element that wraps an `NgFor` element

##### Repeating Items with NgFor

1. Add a method to the component class that returns the value `NgFor` should track.

```typescript
trackByItems(index: number, item: Item): number { return item.id; }
```

2. In the `NgFor`, set `trackBy` to the `trackByItems()` method

```html
<div *ngFor="let item of items; trackBy: trackByItems">
  ({{item.id}}) {{item.name}}
</div>
```

#### NgSwitch

Like the `switch` statement, it can display one element from several based on a switch condition.

1. In the parent element like <div>, add `[ngSwitch]` bound to an expression that returns the switch value. Then bound `*ngSwitchCase` and `*ngSwitchDefault` on the elements for the cases

   ```html
   <div [ngSwitch]="currentItem.feature">
     <app-stout-item    *ngSwitchCase="'stout'"    [item]="currentItem"></app-stout-item>
     <app-device-item   *ngSwitchCase="'slim'"     [item]="currentItem"></app-device-item>
     <app-lost-item     *ngSwitchCase="'vintage'"  [item]="currentItem"></app-lost-item>
     <app-best-item     *ngSwitchCase="'bright'"   [item]="currentItem"></app-best-item>
   <!-- . . . -->
     <app-unknown-item  *ngSwitchDefault           [item]="currentItem"></app-unknown-item>
   </div>
   ```

2. In the `app.component.ts` , define `currentItem` to use it in the `ngSwitch` expression

   ```ts
   currentItem!: Item;
   ```

3. In each child component, add an `item` input property which is bound to the `currentItem` of the parent component. 

   ```tsx
   export class StoutItemComponent {
     @Input() item!: Item;
   }
   ```

## Dependency Injection

Dependencies are services or objects that a class needs to perform its function.

### Creating an Injectable Service

To generate a `HeroService` in the `src/app/heroes` folder, use the command:

```bash
ng generate service heroes/hero
```

Then, go to the hero mock data and add a `getHeroes()` method that returns the heroes from `mock.heroes.ts`

```tsx
import { Injectable } from '@angular/core';
import { HEROES } from './mock-heroes';

@Injectable({
  // declares that this service should be created
  // by the root application injector.
  providedIn: 'root',
})
export class HeroService {
  getHeroes() { return HEROES; }
}
```

### Injecting Services

Injecting Services makes then visible to a component.

The dependency must be injected in the component's `constructor()` function parameters

```tsx
constructor(private heroService: HeroService)
```

### Using Services in Other Services

In this example, assume that `HeroService` depends on a `Logger` service.

Import the `Logger` service and inject in in `HeroService`'s `constructor()`.

```tsx
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class Logger {
  logs: string[] = []; // capture logs for testing

  log(message: string) {
    this.logs.push(message);
    console.log(message);
  }
}
```

```tsx
import { Injectable } from '@angular/core';
import { HEROES } from './mock-heroes';
import { Logger } from '../logger.service';

@Injectable({
  providedIn: 'root',
})
export class HeroService {

  constructor(private logger: Logger) {  }

  getHeroes() {
    this.logger.log('Getting heroes ...');
    return HEROES;
  }
}
```

