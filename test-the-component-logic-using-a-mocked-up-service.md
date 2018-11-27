# 8. Test the Component logic using a mocked up Service

* Add an Name interface

  {% code-tabs %}
  {% code-tabs-item title="src/app/app.models.ts" %}
  ```text
  export interface Name {
    name: string;
  }
  ```
  {% endcode-tabs-item %}
  {% endcode-tabs %}

* Add a simple service.

```text
ng g service app
```

{% code-tabs %}
{% code-tabs-item title="src/app/app.service.spec.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { of, Observable } from 'rxjs';

import { Name } from './app.models';

@Injectable({
  providedIn: 'root'
})
export class AppService {
  constructor() {}

  getCompanies(): Observable<Name[]> {
    return of([
      { name: 'Duncan' },
      { name: 'Sarah' }
    ]);
  }
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Add injected service and new method to getNames\(\) to the AppComponet

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';
import { Observable } from 'rxjs';

import { AppService } from './app.service';
import { Name } from './app.models';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit{
  title = 'testing';
  names$: Observable<Name[]>;

  constructor(private appService: AppService) {}

  ngOnInit(): void {
    this.getNames();
  }

  getNames() {
    this.names$ = this.appService.getCompanies();
  }

}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Add a 'BeforeEach' section before the tests. This will run before each test \('it' sections\).

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
import { AppComponent } from './app.component';
import { of } from 'rxjs';
import { AppService } from './app.service';

describe(`Component: App Component`, () => {
  let appService: AppService;
  let component: AppComponent;

  beforeEach(() => {
    fakeAppService = { getNames: () => of([{ name: 'FAKE_NAME' }]) };
    component = new AppComponent(appService);
  });

  it('add 1+1 - PASS', () => {
    expect(1 + 1).toEqual(2);
  });

  it(`title equals 'testing'`, () => {
    expect(component.title).toEqual('testing');
  });
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Add another test for the names$ property

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
import { of } from 'rxjs';

import { AppComponent } from './app.component';
import { AppService } from './app.service';
import { Name } from './app.models';

describe(`Component: App Component`, () => {
  let appService: AppService;
  let component: AppComponent;

  beforeEach(() => {
    appService = { getNames: () => of([{ name: 'FAKE_NAME' }]) };
    component = new AppComponent(appService);
  });

  it('add 1+1 - PASS', () => {
    expect(1 + 1).toEqual(2);
  });

  it(`title equals 'testing'`, () => {
    expect(component.title).toEqual('testing');
  });

  it(`companyCount = 1`, () => {
    component.ngOnInit();
    component.names$.subscribe((names: Name[]) => {
      expect(names).toEqual([{ name: 'FAKE_NAME' }]);
    });
  });
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

