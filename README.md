# Angular7_Examples_and_CheatSheet
Angular 7 projects for begginers.
Tools needed for work with Angular 7:
- [Node.js](https://nodejs.org/es/): Platform to manage web apps packages and dependencies.
- Angular CLI: Angular Command Line Interface, is a tool that help up to work with Angular.
- TypeScript: A front end typed language to generate JavaScript code.
- Http-server: http-server is a simple, zero-configuration command-line http server. It is powerful enough for production usage, but it's simple and hackable enough to be used for testing, local development, and learning
- Bootstrap
- Firebase (*): A data base manager

The first step is install Node in your machine. Node will help us to install packages and dependencies.
When Node is installed in your mahine you can verify it from command line. It is possible too verify the Node Package Manager (NPM) version, that is the main Node tool.

```command
node -v
npm --v
```

Use Node to install Angular Command Line Interface (Angualr CLI). The Angular structure project is a little confused for begginers and require several files interaction. Angular CLI instructions help to theses functions.

```command
npm install -g @angular/cli
```

To update it
```command
npm uninstall -g @angular/cli
npm cache verify
npm install -g @angular/cli@latest
```
To can test the application distribution version is necessary use the Http-server module from Node
```command
npm install -g http-server
```

Inside the project folder chosen use Angular CLI (ng) command to create a project. A comoponent app.component is created and added to app.module automatically when the project is created.

```command
ng new firstAngular7Project
```

To run the project use the comand into folder project. The "-o" instruction open the main browser with the app page
```command
ng serve
ng serve -o
```

Angular CLIs build a project automatically and with serve command we can see de applicaton running. Only with 2 instructions!

It is possible change the tab icon image.

`````html
<!-- Inside  index.html -->
<head>
    <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
`````

## 1. Angular applications parts
### 1.1. Compoments
It is a decorated class with the decorator @Component joined to a template. The decorater is the application part that define a behavior. A component is divided in several files

````command
app.myComponentName.css
app.myComponentName.html
app.myComponentName.spec.ts
app.myComponentName.ts
````
To create a component:

```` command
ng g c componentName
````

This action will create a folder, the 4 component files and add it to the application module

In the ts file the behavior is defined

```` typescript
//Inside app.myComponentName.ts
import {Component} from '@angular/core';

@Component({
    selector : 'app-myComponentName',
    templateUrl : './app.myComponentName.html',
    styleUrls : ['./app.myComponentName.css']
})
export class AppComponent{
    title = 'First Angular Project';
}
````
Angular project has a global style file "style.css".
It is possible access to component variables from code with the double bracers {{}}, it is called interpolation. According under code, it is possible get title value from the component ussing {{title}}, inside component html file.

```` html
<!-- Inside app.myComponentName.html-->
<div>
    <h1> Welcome to {{title}} </h1>
</div>
````

Angular is used to create SPA (Single Page Applications), it use a index.html where are invoked all components. The way to get the component in the html file is using his directive, the tag associated to the component (selector). The directives help to change the tag apparience and behavior. The main component is the app.component, and it is used in index.html.

```` html
<!-- Inside app.component.html-->
<app-myComponentName></app-myComponentName>
````

To navigate enter components use **routerLink** attribute instead href attribute into a tag.

In **app-routing** file is defined the components mapping

To add eventListener relationship with component function, wrap the event into bracers like this:
```` html
<!-- Inside component.html-->
<button (click)="firstClick()">Click me!</button>
````

It is possible access to component variables/attributes using **braces []** into the tag.
```` html
<!-- Inside component.html-->
<h1 [class.gray]="h1Style">Hello</h1>
<h1 [ngClass]="h1Style">Hello</h1>
<h1 [ngStyle]="h1Style ? 'gray' : 'black'">Hello</h1>
<h1 [ngStyle]="{
        'color' : h1Style ? 'gray' : 'black',
        'font-size' : !h1Style ? '1em' : '4em'
    }">Hello</h1>
````

And it is possible evaluate variables into tags using angular keywords for functions like *ngIf, *ngFor.
```` html
<!-- Inside component.html-->
<div *ngIf="submitted && messageForm.controls.name.errors" class="error">
    <div *ngIf="messageForm.controls.name.errors.required" class="error">Your name is required</div>
</div>
````

To work with formularies angular provide muliple libraries to help us, all of them are include in a module that must be imported in module.app file and the libraries into the component Typescript file.
```` typescript
//Inside app.module.ts
import { ReactiveFormsModule } from '@angular/forms'
````
```` typescript
//Inside app.component.ts
import { FormBuilder, FormGroup, Validators } from '@angular/forms'
````

Differences between **constructor()** and **ngOnInit()**
- **constructor** is invoked only one time when the component is instantied. Used to simple variables initialize and dependencies inyection
- **ngOnInit** is invoked only one time after constructor. Used to complex variables initialize and get properties values

### 1.2. Modules
The module has the control of everything in the application. It is where the components are declared, external modules are imported, and dependencies/providers are added.

```` typescript
//Inside app.module.ts
@NgModule({
    declarations : [AppComponent],
    imports : [BrowserModule, AppRoutingModule],
    providers : [],
    bootstrap : [AppComponent]
})
export class AppModule{}
````

### 2. Firebase and Bootstrap
Cloudfirestore is a Firebase data base. It is a free data base for personal use (no professional). To install all dependencies.

```` command
npm install firebase @angular/fire font-awesome bootstrap @ng-bootstrap/ng-bootstrap --save
````

- firebase to work with firebase
- @angular/fire to work with firebase in angular
- font-awasome to show icons in the application (bootstrap 4 no manage icons)
- bootstrap for CSS (bootstrap 4)
- @ng-bootstrap convert the bootsrap components in angular components

Create a Firebase project from the web (console section), after this is possible creeate a data base from Develop>Database left menu (trail mode). The data base will be Cloud Firestore (trail mode).
Cload Firestore let us have data bases noSQL in the cloud. This data base work with json structures, similar to MongoDB. Each register is like a text document. The files build a collection, but the files content can be differents.
To add the cloud store data base to the angular project is neccesary add the data bases credentias. It are getting from firebase web. The credentials must be copy and added to the environment.ts file into the angular project.
```` typescript
export const environment = {
    production : false,
    firebase : {
        //Credentials here
    }
}
````
After add credentiales is necessary to configure firebase modules into application module in app.module.ts
```` typescript
//Inside app.module.ts
import {AngularFireModule} from '@angular/fire';
import {AngularFirestoreModule} from '@angular/fire/firestore';
import {environment} from 'src/environments/environment';

import {NgbModule} from '@ng-bootstrap/ng-bootstrap';
import {ReactiveFormsModule} from '@angular/forms';

@NgModule({
    declarations : [AppComponent],
    imports : [
        BrowserModule,
        AppRoutingModule,
        AngularFireModule.initializeApp(environment.firebase), //init module with environment properties
        AngularFirestoreModule,
        NgbModule, //bootstrap module
        ReactiveFormsModule
        ],
    providers : [],
    bootstrap : [AppComponent]
})
export class AppModule{}
````

For CSS is necessary review angular.json file. In styles property is defined the CSS file for the project, bootsrap file must be added
```` json
"styles":[
    "node_modules/bootstrap/dist/css/bootstrap.min.css",
    "src/style.css"
]
````

### 3. Node and Node Package Manager (NPM)
| Command                     | Description                                                                                                                                  |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| node -v                     | Returns the Node version                                                                                                                     |
| npm --v                     | Returns the NPM version                                                                                                                      |
| npm install -g @angular/cli | Install Angular CLI for all (-g)                                                                                                             |
| npm install -g http-server  | Install Http Server module for all (-g)                                                                                                      |
| http-server -o              | Deploy the distribution application version and open the application (-o). Must execute the command into the folder distribution application |


### 4. Angular CLI commands
| Command              | Description                                                                                                       |
| -------------------- | ----------------------------------------------------------------------------------------------------------------- |
| ng                   | Return all Angular commands                                                                                       |
| ng version           | Return the Angular CLI and angular components version                                                             |
| ng new "projectName" | Creates Angular project                                                                                           |
| ng serve -o          | Compile the project and run the server (serve) and open the project (-o)                                          |
| ng g c "name"        | Creates a Angular component and add it to the app.module. It is a short command of "ng generate component "name"" |
| ng g s "name"        | Creates a Angular service and add it to the app.module. It is a short command of "ng generate service "name""     |
| ng build             | Creates a dist folder and creates the distribution app files                                                      |
| ng build --prod      | Creates a dist folder and creates the production distribution app files with the min size                         |
