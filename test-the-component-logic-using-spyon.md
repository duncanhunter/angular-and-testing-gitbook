# 9. Test the Component logic using SpyOn

SpyOn is a Jasmine feature that allows dynamically intercepting the calls to a function and change its result. This example shows how spyOn works, even if we are still mocking up our service.

* Change the Mockup service so getNames returns nothing

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
...

  beforeEach(() => {
    appService = { getNames: () => of([]) };
    component = new AppComponent(fakeAppService);
  });
  
...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Add a new Test case

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
    appService = { getNames: () => of([]) };
    component = new AppComponent(appService);
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

