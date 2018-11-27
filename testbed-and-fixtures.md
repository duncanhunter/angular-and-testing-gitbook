# 10. TestBed and Fixtures

The TestBed is the first and largest of the Angular testing utilities. It creates an Angular testing module — a @NgModule class — that you configure with the configureTestingModule method to produce the module environment for the class you want to test.

* Remove the newed up AppComponent and replace it with a TestBed module

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
import { of } from 'rxjs';
import { AppComponent } from './app.component';
import { TestBed, ComponentFixture } from '@angular/core/testing';

import { AppService } from './app.service';
import { Name } from './app.models';

describe(`Component: App Component`, () => {
  let appService: AppService;
  let fixture: ComponentFixture<AppComponent>
  let component: AppComponent;

  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [AppComponent],
      providers: [
        {
          provide: AppService,
          useValue: { getNames: () => (of([])) }
        }
      ]
    });
    fixture = TestBed.createComponent(AppComponent);
    component = fixture.componentInstance;
    appService = TestBed.get(AppService);
  });

  it('add 1+1 - PASS', () => {
    expect(1 + 1).toEqual(2);
  });

  it(`title equals 'testing'`, () => {
    expect(component.title).toEqual('testing');
  });

  it(`Expect service to return a single name`, () => {
    component.ngOnInit();
    component.names$.subscribe((names: Name[]) => {
      expect(names).toEqual([]);
    });
  });

  it(`Expect service to return a single name`, () => {
    const fakeNames = [{ name: 'FAKE_NAME' }];
    spyOn(appService, 'getNames').and.returnValue(of(fakeNames));
    component.ngOnInit();

    component.names$.subscribe((names: Name[]) => {
      expect(names).toEqual(fakeNames);
    });
  });
});

```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now we have a test that runs against a completely mocked up AppComponent bundled with its dependencies. The fixture creates the component just like it the browser would in real life. Using DebugElement, you can even query the DOM for further tests.

* Update the component DOM to add an ID
* Create a new test to query the DOM

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.html" %}
```markup
<ul>
  <li *ngFor="let item of names$ | async">{{item.name}}</li>
</ul>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
  ...
  it(`HTML should have FAKE_NAME in li`, () => {
    const fakeNames = [{ name: 'FAKE_NAME' }];
    spyOn(appService, 'getNames').and.returnValue(of(fakeNames));
    component.ngOnInit();
    fixture.detectChanges();
    const el = fixture.debugElement.query(By.css('li')).nativeElement;
    expect(el.textContent).toEqual('FAKE_NAME');
  });
  ...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

