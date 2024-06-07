# Using Copilot for UI Development - Angular

## Overview

Copilot is a great tool to help with Angular UI development, especially since all of this knowledge would be part of an LLM by virtue of the fact this tool has been around for years.  

This is a great way to learn and improve on your Angular skills.  Copilot can help you with generating code snippets, providing suggestions, and even writing entire functions or components. 

### Lab Objectives

We have already built a DOTNET Core API that provides data for a reports page.  We will use Copilot to help us build an Angular application that will consume this API and display the data in a table.  We will also style the page and add routing to the reports page.

### Prerequisites

- Basic knowledge of Angular
- Angular CLI installed
- Node.js installed
- DOTNET Core API that provides data for the reports page

### Lab Environment

- **OS Used:** Windows 10
- **IDE:** Visual Studio Code
- **Angular Version:** 17

### Angular Application Setup


1. Create a new Angular application using the Angular CLI:

```bash
ng new myapp --standalone false
cd myapp
```
As a sanity check, you can run the application using the following command:

```bash 
ng serve
```

Now we can move on and do the more interesting stuff.

### Report Application

**CoPilot:** I have created an angular app with the following command: ng new myapp --standalone false, using angular version 17. This app needs to add a reports page.  On that page it will make a rest call to: http://localhost:5169/Reports/getInvoices.  This returns JSON in an array where each element contains: billingCountry, invoiceCount.  Display the JSON in an HTML table.  Style the Page with a blue background and yellow text.  Alternate lighter and darker shades of gray on the table.  Define a route to the report page.  Generate all ng commands and code for this application

GitHub Copilot: First, let's outline the steps to achieve your requirements:

1. **Generate Components and Services:**
   - Generate a component for the reports page.
   - Generate a service for making the REST call.

2. **Modify the Service:**
   - Implement the method to make the HTTP GET request to the specified URL.

3. **Modify the Reports Component:**
   - Inject the service and call the method to fetch data on component initialization.
   - Store the fetched data in a variable.
   - Use the variable to display data in an HTML table.

4. **Styling:**
   - Add styles for the page background, text color, and alternating table row colors.

5. **Routing:**
   - Add a route for the reports page in the AppRoutingModule.

6. **Commands to Run:**
   - List of Angular CLI commands to generate the required components, services, and modify routing.

### Step-by-Step Implementation:

#### 1. Generate Components and Services:

```plaintext
ng generate component reports
ng generate service reports
```

#### 2. Modify the Service (`reports.service.ts`):

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn:

 '

root'
})
export class ReportsService {
  private apiUrl = 'http://localhost:5169/Reports/getInvoices';

  constructor(private http: HttpClient) { }

  getInvoices(): Observable<any[]> {
    return this.http.get<any[]>(this.apiUrl);
  }
}
```

#### 3. Modify the Reports Component (`reports.component.ts`):

```typescript
import { Component, OnInit } from '@angular/core';
import { ReportsService } from './reports.service';

@Component({
  selector: 'app-reports',
  templateUrl: './reports.component.html',
  styleUrls: ['./reports.component.css']
})
export class ReportsComponent implements OnInit {
  invoices: any[] = [];

  constructor(private reportsService: ReportsService) { }

  ngOnInit(): void {
    this.reportsService.getInvoices().subscribe(data => {
      this.invoices = data;
    });
  }
}
```

#### 4. Styling (`reports.component.css`):

```css
:host {
  background-color: blue;
  color: yellow;
}

table {
  width: 100%;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

tr:nth-child(odd) {
  background-color: #d9d9d9;
}
```
```bash
 ng serve
```

This generate an error, you have to specifically prompt for routing to the app in the Angular Framework.  I took the error message pasted directly into CoPilot.

#### 5. Routing ([`app-routing.module.ts`](command:_github.copilot.openSymbolFromReferences?%5B%7B%22%24mid%22%3A1%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fjohndohoney%2FDocuments%2Ftungsten%2Fmyapp%2Fsrc%2Fapp%2Fapp-routing.module.ts%22%2C%22scheme%22%3A%22file%22%7D%2C%7B%22line%22%3A0%2C%22character%22%3A0%7D%5D "myapp/src/app/app-routing.module.ts")):

Add the route for the reports page.

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { ReportsComponent } from './reports/reports.component';

const routes: Routes = [
  { path: 'reports', component: ReportsComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

#### 6. HTML for Reports Component (`reports.component.html`):

```html
<table>
  <tr>
    <th>Billing Country</th>
    <th>Invoice Count</th>
  </tr>
  <tr *ngFor="let invoice of invoices">
    <td>{{invoice.billingCountry}}</td>
    <td>{{invoice.invoiceCount}}</td>
  </tr>
</table>
```

#### Commands to Run:

1. Generate the reports component: `ng generate component reports`
2. Generate the reports service: `ng generate service reports`
3. Modify the [`app-routing.module.ts`](command:_github.copilot.openSymbolFromReferences?%5B%7B%22%24mid%22%3A1%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fjohndohoney%2FDocuments%2Ftungsten%2Fmyapp%2Fsrc%2Fapp%2Fapp-routing.module.ts%22%2C%22scheme%22%3A%22file%22%7D%2C%7B%22line%22%3A0%2C%22character%22%3A0%7D%5D "myapp/src/app/app-routing.module.ts") to include the route for the reports page.

This plan covers all the steps and code needed to add a reports page to your Angular application that fetches and displays data from a REST API.

```bash
ng serve
```

johndohoneyjr: core.mjs:6531  ERROR NullInjectorError: NullInjectorError: No provider for _HttpClient!
    at NullInjector.get (core.mjs:1654:27)
    at R3Injector.get (core.mjs:3093:33)
    at R3Injector.get (core.mjs:3093:33)
    at injectInjectorOnly (core.mjs:1100:40)
    at Module.ɵɵinject (core.mjs:1106:42)
    at Object.ReportsService_Factory [as factory] (reports.service.ts:8:28)
    at core.mjs:3219:47
    at runInInjectorProfilerContext (core.mjs:866:9)
    at R3Injector.hydrate (core.mjs:3218:21)
    at R3Injector.get (core.mjs:3082:33)

GitHub Copilot: The error you're encountering, `NullInjectorError: No provider for HttpClient!`, indicates that the `HttpClientModule` has not been imported in your application module. This module provides the `HttpClient` service, which is necessary for making HTTP requests.

To resolve this error, you need to import `HttpClientModule` into your application's main module (usually `app.module.ts`). Here's how you can do it:

1. **Import `HttpClientModule` in `app.module.ts`:**

First, import `HttpClientModule` from `@angular/common/http` at the top of your `app.module.ts` file.

2. **Add `HttpClientModule` to the [`imports`](command:_github.copilot.openSymbolFromReferences?%5B%7B%22%24mid%22%3A1%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fjohndohoney%2FDocuments%2Ftungsten%2Fmyapp%2Fnode_modules%2F%40angular%2Fcore%2Findex.d.ts%22%2C%22scheme%22%3A%22file%22%7D%2C%7B%22line%22%3A7063%2C%22character%22%3A4%7D%5D "myapp/node_modules/@angular/core/index.d.ts") array of `@NgModule` decorator:**

Then, add `HttpClientModule` to the [`imports`](command:_github.copilot.openSymbolFromReferences?%5B%7B%22%24mid%22%3A1%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fjohndohoney%2FDocuments%2Ftungsten%2Fmyapp%2Fnode_modules%2F%40angular%2Fcore%2Findex.d.ts%22%2C%22scheme%22%3A%22file%22%7D%2C%7B%22line%22%3A7063%2C%22character%22%3A4%7D%5D "myapp/node_modules/@angular/core/index.d.ts") array within the `@NgModule` decorator in the same file.

Here's how the updated `app.module.ts` should look:

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http'; // Import HttpClientModule
import { AppComponent } from './app.component';
import { AppRoutingModule } from './app-routing.module'; // Make sure your AppRoutingModule is imported
import { ReportsComponent } from './reports/reports.component'; // Ensure all your components are imported

@NgModule({
  declarations: [
    AppComponent,
    ReportsComponent
    // Add other component declarations here
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule // Add HttpClientModule here
    // Add other modules here
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

By importing `HttpClientModule`, you're making the `HttpClient` service available throughout your application, which resolves the `NullInjectorError` you were facing.

**CoPilot** How can I fix the error "NullInjectorError: No provider for HttpClient!" in my Angular application?

GitHub Copilot: To fix the "NullInjectorError: No provider for HttpClient!" error in your Angular application, you need to ensure that the `HttpClientModule` is imported into your application's main module (usually `app.module.ts`). This module provides the `HttpClient` service, which is necessary for making HTTP requests.

Here's how you can do it:

1. **Import `HttpClientModule` in `app.module.ts`:**

First, import `HttpClientModule` from `@angular/common/http` at the top of your `app.module.ts` file.

2. **Add `HttpClientModule` to the [`imports`](command:_github.copilot.openSymbolFromReferences?%5B%7B%22%24mid%22%3A1%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fjohndohoney%2FDocuments%2Ftungsten%2Fmyapp%2Fnode_modules%2F%40angular%2Fcore%2Findex.d.ts%22%2C%22scheme%22%3A%22file%22%7D%2C%7B%22line%22%3A7063%2C%22character%22%3A4%7D%5D "myapp/node_modules/@angular/core/index.d.ts") array of `@NgModule` decorator:**

Then, add `HttpClientModule` to the [`imports`](command:_github.copilot.openSymbolFromReferences?%5B%7B%22%24mid%22%3A1%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fjohndohoney%2FDocuments%2Ftungsten%2Fmyapp%2Fnode_modules%2F%40angular%2Fcore%2Findex.d.ts%22%2C%22scheme%22%3A%22file%22%7D%2C%7B%22line%22%3A7063%2C%22character%22%3A4%7D%5D "myapp/node_modules/@angular/core/index.d.ts") array within the `@NgModule` decorator in the same file.

Here's an example of how the updated `app.module.ts` should look:

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http'; // Import HttpClientModule
import { AppComponent } from './app.component';
import { AppRoutingModule } from './app-routing.module'; // Assuming AppRoutingModule is already imported
import { ReportsComponent } from './reports/reports.component'; // Import your ReportsComponent

@NgModule({
  declarations: [
    AppComponent,
    ReportsComponent
    // Add other component declarations here
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule // Add HttpClientModule here
    // Add other modules here
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

By importing `HttpClientModule`, you make the `HttpClient` service available throughout your application, which resolves the "NullInjectorError" you were facing.

At this stage the App will work, but you will get a CORS error.  This is because the API is not allowing the Angular App to access the data.  You need to go back to the API and prompt it for adding the code to the startupcs file to allow the Angular App to access the data.


**CoPilot**: Reports/getInvoices' from origin 'http://localhost:4200' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.

GitHub Copilot: The error you're encountering is due to the Cross-Origin Resource Sharing (CORS) policy. This policy prevents web applications running at one origin (domain) from accessing resources from a different origin. Your Angular application running on [`http://localhost:4200`](command:_github.copilot.openSymbolFromReferences?%5B%7B%22%24mid%22%3A1%2C%22path%22%3A%22%2Fc%3A%2FUsers%2Fjohndohoney%2FDocuments%2Ftungsten%2Fmyapp%2Fnode_modules%2F%40angular%2Fcommon%2Fhttp%2Findex.d.ts%22%2C%22scheme%22%3A%22file%22%7D%2C%7B%22line%22%3A7%2C%22character%22%3A0%7D%5D "myapp/node_modules/@angular/common/http/index.d.ts") is trying to access resources from a different origin without the proper CORS headers being present in the response from the server.

To resolve this issue, the server that serves the `/reports/getInvoices` endpoint needs to include the `Access-Control-Allow-Origin` header in its responses, allowing requests from your Angular application's origin.


The remainder of the lab is to go back to the API and prompt it for the code to add to the startupcs file to allow the Angular App to access the data.  This is the code that needs to be added to the startup.cs file in the dotnet API.

When I did get the UI up, the initial selection of styling was not that good, so what follows in an updated CSS.

```css

:host {
  background-color: rgb(0, 234, 255);
  color: black;
  display: flex;
  justify-content: center;
}

table {
  margin-left: auto;
  margin-right: auto;
  width: auto; 
}

td {
  width: 50px;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

tr:nth-child(odd) {
  background-color: #d9d9d9;
}
```

