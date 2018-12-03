# Chat

A live chat project.

## To Run

- Option 1

```bash
ng s --open
```

- Option 2

  Install live-server and serve the build output.

terminal 1

```bash
npm run build::prod

```

terminal 2

```bash
live-server --open=dist/chate/index.html
```

## Goals

- To create a live chat.

## Explanation

- Install @webcomponents/custom-elements

```bash
npm i --save @webcomponents/custom-elements
```

- Copy the following code in pollyfills.ts.

```code
...
/***************************************************************************************************
 * BROWSER POLYFILLS
 */

// Used for browsers with partially native support of Custom Elements
import '@webcomponents/custom-elements/src/native-shim';

// Used for browsers without a native support of Custom Elements
import '@webcomponents/custom-elements/custom-elements.min';

...
/***************************************************************************************************
 * APPLICATION IMPORTS
 */

(window as any).global = window;

```

- Set up angular element in app.module.ts

* Note: that do not boostrap any component in NgModule decorator this will cause error. because we are boostrapping the custom element already in ngDoBoostrap.

```code
...
import { createCustomElement } from '@angular/elements';
...

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, AppRoutingModule],
  entryComponents: [AppComponent],
  providers: []
})

export class AppModule {
  constructor(private injector: Injector) {}

  ngDoBootstrap() {
    const el = createCustomElement(AppComponent, { injector: this.injector });
    customElements.define('chat-app', el);
  }
}
```
