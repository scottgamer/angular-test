# Angular Test App

This is a test app to summarize the main concepts behind Angular

## Installation

- `npm i -g @angular/cli`
- Requires node.js 12

---

## Commands

- ng new [project-name], create new Angular project
- ng serve, start development server
- ng generate component [component-name], create new component

---

## Dynamic Data

### String Interpolation

- Outputs data as text in a template

```html
<p>{{ "Server" }} with ID {{ serverId }} is {{ getServerStatus() }}</p>
```

### Property Binding

- Binds elements properties with class properties
- Changes html properties

```typescript
allowNewServer = false;


  constructor() {
    setTimeout(()=>{
      this.allowNewServer = true;
    }, 2000);
  }
```

```html
<button class="btn btn-primary" [disabled]="!allowNewServer">Add Server</button>
```

### Event Binding

- Binds javascript code to an eventimport { FormsModule } from '@angular/forms';

```html
<button (click)="onCreateServer()">
  Add Server
</button>
```

```typescript
onCreateServer() {
    this.serverCreationStatus = "Server was created";
  }
```

- Using inputs

```typescript
  onUpdateServerName(event: Event) {
    this.serverName = (<HTMLInputElement>event.target).value;
  }
```

```html
<input type="text" class="form-control" (input)="onUpdateServerName($event)" />
<p>{{ serverName }}</p>
```

### Two-way Data Binding

- Allows changin data in both directions html > typescript, typescript > html

- First, enable the `ngModel` directive by adding `FormsModule` to `imports[] in the AppModule`

```typescript
import { FormsModule } from "@angular/forms";
```

```html
<input type="text" class="form-control" [(ngModel)]="serverName" />
<p>{{ serverName }}</p>
```

---

## Directives

- Instructions in the DOM
- Can be used as element attributes

### NgIf

- Displays an element if a condition is met
- It's an structural directive

```html
<p *ngIf="serverCreated">Server was created, server name is {{ serverName }}</p>
```

```typescript
this.serverCreated = false;

onCreateServer() {
    this.serverCreated = true;
    this.serverCreationStatus = `Server was created! Name is ${this.serverName}`;
  }
```

- It is possbile to use if-else

```html
<p *ngIf="serverCreated; else noServer">
  Server was created, server name is {{ serverName }}
</p>
<ng-template #noServer><p>No server was created</p></ng-template>
```

### NgStyle

- Allows to dynamicaly assign an style
- It's an attribute directive
- Can be bound to element attributes

```html
<p [ngStyle]="{color: getColor()}">
  {{ "Server" }} with ID {{ serverId }} is {{ getServerStatus() }}
</p>
```

```typescript
getColor() {
    return this.serverStatus === "online" ? "green" : "red";
  }
```

### NgClass

- Allows to dynamicaly add or remove classes

```html
<p
  [ngStyle]="{ color: getColor() }"
  [ngClass]="{ online: serverStatus === 'online' }"
>
  {{ "Server" }} with ID {{ serverId }} is {{ getServerStatus() }}
</p>
```

```typescript
@Component({
  styles: [
    `
      .online {
        color: white;
      }
    `
  ]
})
export class ServerComponent {
  serverStatus: string = "offline";

  constructor() {
    this.serverStatus = Math.random() > 0.5 ? "online" : "offline";
  }
}
```

---

This project was generated with Angular CLI version 9.0.4.

# Development server

Run ng serve for a dev server. Navigate to http://localhost:4200/. The app will automatically reload if you change any of the source files.

# Code scaffolding

Run ng generate component component-name to generate a new component. You can also use ng generate directive|pipe|service|class|guard|interface|enum|module.

# Build

Run ng build to build the project. The build artifacts will be stored in the dist/ directory. Use the --prod flag for a production build.

# Running unit tests

Run ng test to execute the unit tests via Karma.

# Running end-to-end tests

Run ng e2e to execute the end-to-end tests via Protractor.
