# FirstAngularApp

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 17.3.12.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.

<hr>
<br>
<br>

## Notes:

<br>

## Why would you use Angular?

Angular simplifies the process of building complex, interactive web UI (provides rules, features, concepts)

<hr>

1.
Write declarative code (instead of imperative vanilla js)

Inperative code
Step-by-step instructions (in code) that tell the browser what to do

Example of inperative code (vanilla Js):

1) Find DOM element and store in variable
2) Add event listener to element
3) In triggered function: Find another element
4) Set CSS visibility of that element to 0
5) Create a new `<p>` DOM element
6) Set text content of `<p>` DOM element
7) Find element into which the `<p>` should be inserted
8) Insert `<p>` element

<br>

Declarative code
Define the target UI states and how they change and let Anguler do the rest

Example of declarative code (Angular):

1) Manage "activeTab" state property
2) Depending on "activeTab", show different content
3) Change "activeTab" upon click on tab element

<hr>

2.
Separation of concerns via components

You build a component tree
One Angular App = One Component Tree

Components are "Custom HTML Elements" (Combination of marking, styling and logic)

Why components?

Modular Apps:

1) Break up complex apps into simple building blocks
2) Split up responsibilities and concerns
3) Build a component once and re-use it as often as needed

Better Development Process:

1) Assign different team members to different components
2) Share components and logic across the team
3) Reduce dependencies

<hr>

3.
OOP concepts and principles

<hr>

4.
Use TypeScript

TypeScript is a JavaScript superset - an extension of JavaScript

It extends the JavaScript syntax to support strong and strict typing
Unlike "vanilla JavaScript", TypeScript enforces types and prevents unexpected value type changes

TypeScript is not an Angular feature but can used independently
Angular embraces it though, hence all Angular projects use TypeScript

With TypeScript, you can often catch errors early on during development

<br>

## Dinamic outputs

There are 2 main ways Binding template or parts of template to values generated by the component class:

1) String interpolation - {{ }}

2) Property binding - [property of DOM element] e.g. `<img [src]="value">`

Computing value (construct value of multiple values):

```
export class UserComponent {
  selectedUser = DUMMY_USERS[randomIndex];

  get imagePath() {
    return 'assets/users/' + this.selectedUser.avatar
  }
}
```

get - getter
imagePath() - identifier

Its a method thats usable like a property so that does not need to be called and executed
and thats meant to produce and return a new value

<br>

## Components

When building a component start with exporting class.

Decorator (TypeScript feature which adds metadata to the class):
```
@Component({
  selector: 'app-root',
  standalone: true,
  imports: [RouterOutlet],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
```

selector - tells angular for which elements it should look in the html code, so that those elements
	can be replaced by current component and its markup (template)

Every component have template

!!! All properties that are defined in component class are accessible in component template.

<br>

## Event listener

Add event listener to element in brackets () -> `<button (click)>`

<br>

## Signals

Signals used to notify Angular about value changes and required UI updates

- Requires usage of special "signal" instructions and code

`signal(value)`

- Signals are trackable data containers

- A signal is an object that stores a value (any type of value, including nested objects)

- Angular manages subscriptions to the signal to get notified about value changes

- When a change occurs, Angular is then able to update the part of the UI that needs updations

- To change signal value use set method:
(variable is the signal object with name param)
`variable.set(value)`

- To extract or access the signal value you have to call the signal value as a function:

`{{ variable().name }}`

<br>

- Computed values cannot be created with getter anymore if using signals. Instead, we use computed function from Angular core, which is meant to be used with signals
computed takes the function as an argument, which should return a computed value which may use a signal `computed(() => )`

<br>

Example:

```
export class UserComponent {
    selectedUser = DUMMY_USERS[randomIndex];
    imagePath = computed(() => 'assets/users/' + this.selectedUser().avatar);


  // get imagePath() {
  //   return 'assets/users/' + this.selectedUser.avatar
  // }
}
```
- Computed function under the hood also creates a signal, that why we need to call imagePath as a function:
`<img [src]="imagePath()" [alt]="selectedUser().name" />`

<br>

## Inputs

We use Input decorator to mark a property as setable from outside

`@Input() avatar`
```
<li>
    <app-user [avatar]="users[0].avatar" [name]="users[0].name" />
</li>
```

- In TypeScript if we do not have initial value (we expect value to be set from outside), we have to define/assign type

`@Input() avatar: string;`

- If property has no initializer and is not definitely assigned in the custructor (TypeScript knows that this should be a string, but it does not understand that we are using an Angular mechanism for receiving the value of the property, but TypeScript sees that there is no value being set at any point in this component)

`@Input() avatar!: string;`

- ! mark tells TypeScript that we know that this will definitely be set to some value eventhough TypeScript cant see it

<br>

Input values/properties can be configured by passing config object:

`@Input({required: true}) avatar!: string;`

required: true means that property must be set

<hr>
<br>

## Outputs

We use Output decorator for a property

`@Output() select = new EventEmitter();`

- select is a custom select event
- @Output is a decorator
- EventEmitter will allow to emit custom values through select property to any parent component that interested

- $event is a special Angular variable used in parts where you handle events in templates, that will hold the data/value that was emitted by event you are listening to

Example:

<br>

In UserComponent

```
@Output() select = new EventEmitter();

onSelectUser() {
    this.select.emit(this.id);
  }
```
In AppComponent
```
onSelectUser(id: string) {
    console.log('Selected user with id ' + id);
  }
```
In AppTemplate
```
<li>
    <app-user [id]="users[0].id" [avatar]="users[0].avatar" [name]="users[0].name" (select)="onSelectUser($event)" />
</li>
```
