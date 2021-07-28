[TOC]

# Overview

- React vs. Angular
    + https://technostacks.com/blog/react-vs-angular

- A client-side web development framework
- Angular is a newer version of AngularJS
    + Angular uses TypeScript instead of JavaScript
    + Angular uses a hierarchy of components as its main architectural
      concept
    + Angular uses CLI which reduces development time
    + Angular introduced property binding, event binding, and template
      binding along with template interpolation
- Why Angular?
    + Cross platform
    + Simplified MVC pattern
    + Flexible development
    + single-page Application
    + Speed and performance
    + Data binding and fastest load
- Angular Visioning: semantic versioning
    + Major.Minor.Patch
    + Major: a breaking change, contains significant new features
    + Minor: some new features
    + Patch: low risk, bug fix
- Angular 8
    + Ivy rendering: reduces the size and makes the app 70 times faster
    + Bazel: is an orchestration app which helps to bundle the app
      faster
    + Differential loading: help bundle your app for modern (ES6) or
      legacy (ES5) browsers, with the no change in codes and reducing
      the size by 70% for latest browser
    + Support for TypeScript 3.4 and entire @angular/http package has
      been removed, instead @angular/common/http, a new API which is
      smaller, easier, and more powerfull is used to make HTTP requests
- Angular vs. React vs. Vue.js
    + Angular: Model View View Model; the others only have View
    + Angular: readl DOM; others are virtual DOM
- Angular Architecture
    + Model View ViewModel (MVVM)
    + ViewModel is responsible for maintaining relationship between View
      and Model: 2-way binding
- Building blocks of Angular
    + Modules: a mechanism to group components, directives, pipes and
      services
        * All files are declared inside a module
        * Angular app contains at least one module (root: AppModule)
    + Components: are codes or pages in an application
        * Each component controls one or more section on the screen
        * Every Angular app has at least one component (root:
          AppComponent)
        * Each component contains application data, logic, and a HTML
          template
    + Template: a template modifies HTML elements before they are
      displayed
        * A form of HTML tag that tells Angular about how to render the
          component
    + MetaData: tells Angular where to get the major building blocks
      that it needs to create and present the component and its view
        * It associates a template with the component, either directly
          with inline code, or by reference
    + Directives:
        * Angular transforms the DOM according to the instructions given
          by directives.
        * A component is a directive with a template
        * 2 kinds: structural and attribute directives
    + Data Binding: a mechanism for coordinating parts of a template
      with parts of a component
        * Types: two-way data binding, event binding, property binding
          and string interpolation
    + Services: a class with a well-defined purpose (fetch data from
      server, validate user input)
        * Examples: logging service, data service, message bus, tax
          calculator, application configuration, etc.
    + Dependency Injection: refers to one object supplying the
      dependencies of another object
        * These dependencies define how various components are connected
          and show how changes in one part of the code affects other
          parts
        * Tree-shaking is used to remove dependencies defined by
          dependency injection
- Files Structure in an Angular project: root: project_directory
    + `src`: source codes
        + `app`: contains project's logic and data (components,
          templates, and styles)
        + `assets`: image and other asset files
        + `environements`: contains build configuration options for
          particular target environments
        + `index.html`: main HTML page
        + `main.ts`: compilation starts from thsi file. It bootstraps
          the application's root module to run in the browser
        + `styles.css`: lists CSS files that supply styles
        + `test.ts`: tests
    + `.editorconfig`: maintains consistent coding styles
    + `.gitignore`
    + `angular.json`: Angular application starts executing from this
      file
        * If you are an ADVANCED USER, you can change the ways Angular
          works by modifying this file
    + `package-lock.json`: exact package versions
    + `package.json`: configures npm package dependencies and npm metadata
    + `tsconfig.app.json`: application-specific TypeScript
      configuration, including TypeScript and Angular template compiler
      options
    + `tsconfig.json`: TypeScript configuration
    + `tsconfig.spec.json`: TypeScript configuration for the application
      tests
    + `tslint.json`: application-specific TSLint configuration. TSLint
      is an tool that checks TypeScript code for readability,
      maintainability, and functionality errors.
- Angular App Bootstrapping
    + `main.ts => AppModule => AppComponent`
    + `main.ts`: initializes the platform browser where the app will run
      and bootstrap AppModule
    + `AppModule`: root module bootstraps AppComponent and inserts it
      into the index.html host web page
    + `AppComponent`: root component under which other components are
      nested
        * First component to be inserted into the browser DOM

# Module

- Module Structure: import + decorator + export
    + Import: describes the files that are needed to be imported
    + Decorator: describes the metadata of the application
    + Export: Describes the file that must be exposed to external
      environment

```typescript
import { NgModule } from '@angular/core';
@NgModule({
    imports: [BrowserModule], //imports other modules
    providers: [Logger], // defines services that can be injected
                         // into this module's views
    declarations: [AppComponent], //declares views to make them
                                  //privately available in this module
    exports: [AppComponent], //makes the declared view public, so that
                             //they can be used by other modules
    bootstrap: [AppComponent] // this is set to a root component that
                              // must be launched
})
export class AppModule () {}
```

# Components

- Components are the TypeScript classes that control a patch of screen
  that we call a view (UI) and declare reusable building blocks for an
  application.
- Benefits
    + easy to replicate the logic and style
    + splits the complex application into reusable parts
    + easy to integrate
    + easy to update or add components
- Structure of components
    + Root Component
        * Header Component
            - Search-bar component
            - nav-bar component
            - nva-bar component for the courses
        * Scroll Bar Component
        * Courses Component
- A component: import + decorator + export (class section)
    + Import section
    + Decorator section: it is used to configure the component,
      including things like the selector name and HTML template
    + Export (Class section): it defines the logic of the component

```typescript
import {Component, OnInit} from '@angular/core';
@Component({
    selector: 'app-comp',
    templateUrl: './server.component.html',
    styleUrls: ['./server.component.css']
})
export class serverComponent implements OnInit {}
```

- Create a new component manually:
    + Create a sub directory under `app` directory: `app/server`
    + Create files in the sub directory:
        * `server.component.ts`
        * `server.component.spec.ts`
        * `server.component.html`
        * `server.component.scss`
    + Add the new component to the AppModule
        * open `app.module.ts`
        * import `serverComponent` in AppModule
        * add `serverComponent` to `@NgModule>declarations`
    + Add the new component to the AppComponent
        * open `app.component.html`
        * add `<app-comp></app-comp>`: using the component selector
- Create a new component using CLI
    + `ng generate component server` or `ng g c server`
    + Modify AppModule and AppComponent to add the new component
- `@Component` decorator configuration options
    + `selector`: defines the HTML tag name which is used to add the
      component to the application through HTML
    + `template`: adds inline HTML to define the look of the component
    + `templateUrl`: imports an external template file
    + `styles`: adds inline CSS
    + `styleUrls`: imports an array of external CSS stylesheets
    + `viewProviders`: imports and uses Angular services that provide
      functionalities such as HTTP communications
- Specifying selectors
    + `selector: 'app-element'`: this selector can be used directly in
      the template using HTML tag
    + `selector: '[app-element]'`: can be used as attribute selector
        * `<div app-element></div>`
    + `selector: '.app-element'`: can be used as a class
        * `<div class="app-element"></div>`
    + `selector: '#app-element'`: can be used as an id
        * `<div id="app-element"></div>`
- Template
    + template: `<div> ... </div>`: HTML inside the back ticks
    + templateUrls: './app.component.html',
- Style
    + styles: [`div{color: red;}`, `..`]: an array, each string (between
      back ticks) in the array defines some CSS
    + styleUrls: ['...', '...']: an array of files
- Lifecycle hooks
    + Key life moments of the component and directives
    + `ngOnChanges()`: invoked when there is a change in one or more
      input properties of the component
        * called before `ngOnInit()`
    + `ngOnInit()`: initialize component after Angular first displays
      the data-bound properties and sets the component's input
      properties
        * called once, after the first `ngOnChanges()`
    + `ngDoCheck()`: detect and act upon the changes that Angular can't
      or won't detect on its own
        * called during every change detection run, immediately after
          `ngOnChange()` and `ngOnInit()`
    + `ngOnDestroy()`: called just before Angular destroys the component
        * cleanup process, unsubscribe Observables and detach event
          handlers to avoid memory leaks.
    + `ngAfterContentInit()`: invoked after Angular projects external
      content into the component's view
        * called once after the first `ngDoCheck()`
    + `ngAfterContentChecked()`: invoked after Angular checks the
      content projected into the component
        * called after the `ngAfterContentInit()` and every subsequent
          `ngDoCheck()`
    + `ngAfterViewInit()`: respond after Angular initializes the
      component's views and child views
        * called once, after the first `ngAfterContentChecked()`
    + `ngAfterViewChecked()`: respond after Angular checks the
      component's views and child views
        * called after the `ngAfterViewInit()` and every subsequent
          `ngAfterContentChecked()`


# Data Binding

- Data binding is communication between the TypeScript code / business
  logic of the component and the template (UI).
- Types
    + One-way binding: M to V or vice versa
        * String interpolation: M == {{value}} ==> V
            - Hardcoded data/value inside a component should be
              displayed directly on the view
            - Cannot use multi-line expression
            - Only works with string
        * Property binding: M == [property]="value" ==> V
            - Bind data in Model to a property of an HTML element
            - Works with other data types
        * Event binding: V == (event) = "eventHandler()" ==> M
            - Handles user interaction with an application
            - `(click)="addToCart(item)`
    + Two-way binding: M `<== [(ngModel)] ==>` V
        + a combination of property and event binding. It is a
          continuous synchronization of data from view to the component
          and vice versa
        + Angular provides us a directive: `ngModel` directive
- Types of component interaction: Component1 ==> HTML ==> Component2
    + `@Input()` decorator: passes data from the parent component to the
      child component
        * In the parent component create a `parentProperty` and assign
          value to it (parent.component.ts)
            - `public parentProperty = "value";`
        * Inside the selector of the child's component, bind the
          `parentProperty` to `childProperty` (parent.component.html)
            - `<prefix-parent-comp [childProperty]="parentProperty"></prefix-parent-comp>`
        * In the child component use `@Input()` decorator to receive
          `parentProperty` and locally assign it to `childProperty`
            - `@Input('parentProperty') public childProperty;`
    + `@Output()` decorator: passes data from the child component to the
      parent component
        * In the child component create a new instance of the
          `EventEmitter` class
            - `@Output() public childEvent = new EventEmitter();`
        * In the child component define a method `fireEvent` and emit
          a message
            - `fireEvent(){this.childEvent.emit("message");}`
        * Use `$event` to capture this event in the HTML template of the
          parent component
            - `<prefix-child-component (childEvent)="message=$event"></prefix-child-component>`
    + Services: when there is no parent child relation, we can use
      Angular service
    + Routes: switch from one view to the next as users perform tasks

# Directives

- Directives give instructions to change the DOM
    + Extend HTML with new attributes
    + Transform DOM according to instructions
    + Appear within HTML tag
    + Modify JavaScript classes
- Other Use cases
    + Adapt third party codes to Angular
- Types of directives:
    + Components: directives with templates
    + Structural directives:
        * `*ngIf`: conditionally creates or disposes of subviews from
          the template
        * `*ngFor`: repeat a node (DOM tree) for each item in a list
        * `*ngSwitch`: switch among alternative views
        * Cannot have more than one structural directive on one single
          element, so we need to wrap the element by `<ng-container>`
    + Attribute directives:
        * `ngModel`: adds two-way data binding to an HTML form element
        * `ngStyle`: adds and removes a set of HTML styles
            - used if want to change one style
            - if want to change multiple styles, `ngClass` is best
        * `ngClass`: adds and removes a set of CSS classes
            - value of `[ngClass]` can be a string, an object, or an
              array
        * Can have more than one attribute directive
    + Custom structural/attribute directives
        * You can create your own custom directives
        * Can be use to integrate third-party libraries
        * `ng generate directive <path/name>`
- `*ngIf`

```html
<div *ngIf="booleanCondition; else elseTemplate">content</div>
<ng-template #elseTemplate>
    <div>Else Content</div>
    <div *ngIf="innerCondition; else innerTemplate">content</div>
</ng-template>
<ng-template #innerTemplate>
    <div>Inner else</div>
</ng-template>
```

- `*ngFor`

```html
<ul>
    <ng-container *ngFor="let course of courses">
        <li *ngIf="course.price < 20000">
        {{course.name}}:{{course.price}}
        </li>
    </ng-container>
</ul>
```

- `*ngSwitch`

```html
<div [ngSwitch]="courses">
    <p *ngSwitchCase="'aws'">Aws Architect</p>
    <p *ngSwitchCase="'angular'">Angular Certification Training</p>
    <p *ngSwitchDefault="'RPA'">RPA Using UIpath</p>
</div>
```

- `[ngClass]`

```html
<button [ngClass]="['btn', 'btn-primary']">
<button [ngClass]="'btn btn-primary'">
<button [ngClass]="{'btn': course.category === 'RPA', 'btn-primary': true}">
```

- `[ngStyle]`

```html
<input [(ngModel)]="color" />
<button (click)="size = size + 1">+</button>
<button (click)="size = size - 1">+</button>
<div [ngStyle]="{'color': color, 'font-size': size + 'px'}"></div>
```

- A custom directive

```typescript
import { Directive, ElementRef, HostListener } from '@angular/core';
@Directive({
    selector: '[appCustomdirective]
});
export class CustomdirectiveDirective {
    constructor(private elementRef: ElementRef) {}
    @HostListener('mouseenter') onMouseEnter() {
        this.elementRef.nativeElement.style.backgroundColor='grey';
    }
    @HostListener('mouseleave') onMouseLeave() {
        this.elementRef.nativeElement.style.backgroundColor='';
    }
}
```
```html
<ul>
    <li *ngFor="let course of courses" appCustomdirective>
    {{course.name}}
    </li>
</ul>
```

# Pipes

- Pipes transform output in the template.
    + It is denoted by the symbol `|`
    + It takes numbers, strings, arrays and date as input and converts
      them in the required format to display it on browser.
- To use pipes for `ngModel`, two-way data binding, we can use `ngModel`
  and `ngModelChange` together

```html

```
- Built-in pipes:
    + String: LowerCasePipe (lowercase), UpperCasePipe (uppercase),
      TitleCasePipe (titlecase), SlicePipe (slice: idx1:idx2)
    + Number:
        * DecimalPipe: `{{value_expr | number [:'digits']}}`
            - `digits`: minDigits.minFractionDigits-maxFractionDigits
            - `{{data | number: 2.2-4}}`
        * PercentPipe: `{{value_expr | percent}}`
        * CurrencyPipe: `{{value_expr | currency [:symbol:digits]}}`
            - `{{data | currency:'symbol-narrow':2.2-2}}`
        * DatePipe: `{{value_expr | date: 'shortDate'}}`
    + Pipes can be chain together
- Custom pipes
    + `ng generate pipe <path/name>`
    + Add custom pipe to AppModule: `import {CustompipePipe} from ...;`
        * `declarations: [..., CustompipePipe, ...]`

```typescript
import { Pipe, PipeTransform } from '@angular/core';
@Pipe({
    name: 'custompipe'
})
export class CustompipePipe implements PipeTransform {
    transform(value: any, ...args: any[]): any {
        // implement pipe logic here
        return null;
    }
}
```

- Pure vs. Impure Pipes
    + Pure pipes get executed when it detects changes in the value
      expression, if the value is an object, the changes of object's
      properties do not trigger the pure pipes. We need impure pipes if
      you want the pipes to get executed when the properties get
      changing.

# Services

-

# Routers

- Switch between pages / views
    + Based on URL, routes to different components
- Terms
    + Routes: an array of routes, each mapping a URL to a component
    + Router: the primary infrastructure piece that actually provides
      component navigation
    + RouterLink: the directive for binding a clickable HTML element to
      a route. Clicking an element with a RouterLink trigger a
      navigation.
    + RouterOutlet: a directive marks where the router displays a view
- Route Properties
    + path: a string, or wildcard matcher
    + component: reference to a component
    + redirectTo: a string of another valid route
    + pathMatch: 'full', 'prefix', matching strategy
    + children: an array of child routes
    + outlet: string of named outlet, tells the route to load in a
      specific router outlet
    + canActivate:
    + canDeactivate:


# Best Practices

- Angular application folder structure
    + https://www.tektutorialshub.com/angular/angular-folder-structure-best-practices/
    + https://medium.com/dev-jam/5-tips-best-practices-to-organize-your-angular-project-e900db08702e

```text
- project
    + data
        * db.json
    + src
        * app
            - core
                + models
                    * index.ts (use to simplify imports)
                    * model-1.ts
                    * model-2.ts
                + services
                    * index.ts (use to simplify imports)
                    * service-1.ts
                    * service-2.ts
                + core.module.ts
                + index.ts (use to simplify imports)
            - shared
                + components
                    * index.ts (use to simplify imports)
                    * footer (component)
                    * header (component)
                + shared.module.ts
                + index.ts
            - module1 (admin)
                + components
                    * component1
                    * component2
                + directives
                    * custom1.directive.ts
                + pipes
                    * custom1.pipe.ts
                + validators
                    * custom1.validator.ts
                + module1.module.ts
                + module1-routing.module.ts
                + index.ts
            - page-not-found (component)
            - app.module.ts
            - app-routing.module.ts
        * asset
            - i18n
                + lang-a.json
                + lang-b.json
            - images
                + image-a.svg
                + image-b.svg
            - static
                + structure-a.json
                + structure-b.json
            - icons
                + custom-icon-a.svg
                + custom-icon-b.svg
        * environments
            - environment.prod.ts
            - environment.ts
        * styles
            - app-loading.scss
            - company-colors.scss
            - variables.scss
        * styles.scss
        * main.ts
        * test.ts
        * polyfills.ts
        * index.html
        * favicon.ico
```

- Style guide: https://angular.io/guide/styleguide
- Initialize class members in declarations
    + Only initialize class members in constructors if the members
      require data that is passed through constructors' parameters
- Keep constructor minimal
    + Use it for dependency injection (inject services) and initialize
      class members which require external values
- `ngOnInit()`: all work that you want to do after the class (components,
  directives, etc.) has been created
    + fetch data, major work, etc.

# Libraries

## RxJS (Reactive Programming)

- Provides observable and observer

## Bootstrap CSS

- Directly use Bootstrap CSS
    + `npm install bootstrap`
    + import bootstrap in `styles.scss`
- `ng-bootstrap`: https://ng-bootstrap.github.io/#/home

# Tutorials

## Basic Angular CLI

- Installation Angular CLI
    + `npm install -g @angular/cli`: install angular CLI globally
- Usage:
    + `ng new <project_name> --prefix <prefix>`: create a new project
      with a prefix to prevent name collision
    + `ng serve -o`: start the server and open the localhost

## Other libraries

- json-server: `npm install json-server`
    + json-server-auth: `npm install -D json-server json-server-auth`
-

## Animation

- Angular animation (CSS animation)
    + Importing animation module in `app.module.ts`, and animation
      functions in `app.component.ts`
```typescript
// app.module.ts
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
@NgModule({
    imports: [
        ...
        BrowserAminationsModule,
        ...
    ],
    ...
})
```
```typescript
//app.component.ts
import {trigger, state, style, animate, transition} from '@angular/animation';
@Component({
    animations: [
        // animation triggers go here
    ]
});
export const HighlightTrigger = trigger("rowHighlight", [
    state("selected", style({
        backgroundColor: "lightgreen",
        fontSize: "20px"
    })),
    state("notselected", style({
        backgroundColor: "lightsalmon",
        fontSize: "12px"
    })),
    transition("selected => notselected", animate("200ms")),
    transition("notselected => selected", animate("400ms"))
]);
```
