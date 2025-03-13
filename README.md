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

<hr>

Alternative way of creating output

Instead of @Output decorator we use output function from angular/core

`select = output<string>();`

Under the hood, output function also store an EventEmitter, so we do not need to create emitter on your own

- `<string>` the type of value that will be emitted
- select is a event emitter !!! ouput does not create any kind of signal like input function does

Why output function exists?

1) At the end they do the same
2) If you use input functions, you use output function to avoid decorators in component
3) Outer function shorter than decorator

<br>

If you are using @Output decorator approach, you can still add generic type assignment by add angle brackets as input/output functions, to let TypeScript know about the type of value that will be emitted. It is not required, but good practice if we expect the specific type value

`@Output() select = new EventEmitter<string>();`

<br>

## TypeScript: Potential undefined values

- The main thing/advantage TypeScript brings to the table is that it enforces strong and static typing. Which means you have to be clear about which type of value goes where

There is a possibility that user which such id will not be found and return undefined, so that will crash app (Runtime error)

- When you add ! mark, you are not technically ruling out the possibility of getting an undefined value, you just convincing TypeScript that you (developer) know that you will never have undefined value in specific place

<br>

For Example:
```
get selectedUser() {
    return this.users.find((user) => user.id === this.selectedUserId);
  }
```
There you cannot be 100% sure if its not going to be undefined, its better to setup fallback code

`@Input({ required: true }) name!: string;`

into

`@Input() name?: string;`

The ? mark tells TypeScript "Its fine, this might not be set, and i aware of that"

`<app-tasks [name]="selectedUser?.name" />`

So we access name property only if have object
Alternative would be

`<app-tasks [name]="selectedUser ? selectedUser.name : ''" />`

<hr>

Union type

<br>

Alternative syntax for ? mark
Instead of adding a ? mark you could change type on right side of colon, such that you make it clear that the accepted value types of name are either of type string or type of undefined

`@Input() name: string | undefined;`

The | symbol is an operator which creates union type, it tells TypeScript that type of value that can be stored in something is either of type string or type undefined

- We can simplify 3 @Input, by excepting only 1 property (entire user) as all users are made of the same pieces of data

```
@Input({ required: true }) user!: {
    id: string;
    name: string;
    avatar: string;
  };
```

- {} creates an user object type

Object types can become complex, so we should use type alias

```
type User = {
    id: string;
    name: string;
    avatar: string;
}
```
So its created own type User, which can be used in @Input

`@Input({ required: true }) user!: User;`

Alternative way

```
interface User {
    id: string;
    name: string;
    avatar: string;
}
```

<br>

## Dynamic content

Instead of mannually adding/controling data, its nice to dinamically render items that may change

```
@for (user of users; track user.id){
        <li>
            <app-user [user]="user" (select)="onSelectUser($event)" />
        </li>
    }
```

- user is up to you
- users must refer to some property of component class which hold list data
- @for loop must have a track
- track - expression for Angular to reuse rendered list item and does not need to recreate it everytime something changes. With it, we are telling Angular which unique id criteria can be assigned by Angular, automatically behind the scenes, to every list item or element

<hr>

Alternative syntax

```
<li *ngFor="let user of users">
    <app-user [user]="user" (select)="onSelectUser($event)" />
</li>
```

- ngFor should be imported from angular/common in component class and added to imports array
- ngFor is a structural directive. They are enhancements that you can add to elements, that will change those elements, or change the DOM where those elements are used

<br>

## Conditional content

We use @if, @else features to render specific markup only if condition is true

```
@if (selectedUser) {
    <app-tasks [name]="selectedUser.name" />
}
```

<hr>

Alternative syntax

```
<app-tasks *ngIf="selectedUser; else fallback" [name]="selectedUser!.name" />
    <ng-template #fallback>
        <p id="fallback">Select a user to see their tasks!</p>
    </ng-template>
```

- ngIf should be imported from angular/common in component class and added to imports array