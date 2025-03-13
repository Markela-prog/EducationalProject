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
5) Create a new <p> DOM element
6) Set text content of <p> DOM element
7) Find element into which the <p> should be inserted
8) Insert <p> element

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
