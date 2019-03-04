# Angular7_Examples_and_CheatSheet
Angular 7 projects for begginers.
Tools needed for work with Angular 7:
- [Node.js](https://nodejs.org/es/): Platform to manage web apps packages and dependencies.
- Angular CLI: Angular Command Line Interface, is a tool that help up to work with Angular.
- TypeScript: A front end typed language to generate JavaScript code.
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

Inside the project folder chosen use Angular CLI (ng) command to create a project.

```command
ng new firstAngular7Project
```

To run the project use the comand into folder project.
```command
ng serve -o
```

Angular CLIs build a project automatically and with serve command we can see de applicaton running. Only with 2 instructions!

## 1. Angular applications parts
### 1.1. Compoments
It is a decorated class with the decorator @Component joined to a template. The decorater is the application part that define a behavior. A component is divided in several files

````command
app.myComponentName.css
app.myComponentName.html
app.myComponentName.spec.ts
app.myComponentName.ts
````

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

It is possible access to component variables from code with the double bracers {{}}, it is called interpolation. According under code, it is possible get title value from the component ussing {{title}}, inside component html file.

```` html
<!-- Inside app.myComponentName.html-->
<div>
    <h1> Welcome to {{title}} </h1>
</div>
````

Angular is used to create SPA (Single Page Applications), it use a index.html where are invoked all components. The way to get the component in the html file is using his directive, the tag associated to the component (selector). The directives help to change the tag apparience and behavior.

```` html
<!-- Inside index.html-->
<app-myComponentName></app-myComponentName>
````
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

### Node and Node Package Manager (NPM)
| Command                     | Description                      |
| --------------------------- | -------------------------------- |
| node -v                     | Return the Node version          |
| npm --v                     | Return the NPM version           |
| npm install -g @angular/cli | Install Angular CLI for all (-g) |


### Angular CLI commands
| Command              | Description                                           |
| -------------------- | ----------------------------------------------------- |
| ng | Return all Angular commands |
| ng version           | Return the Angular CLI and angular components version |
| ng new "projectName" | Create Angular project                                |
| ng serve -o          | Compile the project and run the server (serve) and open the project (-o)      |
| ng g c "name" | Create a Angular component. It is a short command of "ng generate component "name"" |

)
