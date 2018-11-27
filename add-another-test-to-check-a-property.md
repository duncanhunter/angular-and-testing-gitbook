# 7. Add another test to check a property

* Remove the failing test
* Under the last `it` block add another `it` block and write a test to check the title property is set correctly

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
import { AppComponent } from './app.component';
describe(`Component: App Component`, () => {
  it('add 1+1 - PASS', () => {
        expect(1 + 1).toEqual(2);

  });
  
  it(`title equals 'Angular Superpowers'`, () => {
    const component = new AppComponent();
    expect(component.title).toEqual('testing');
  });
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* set the title accordingly in the component

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
export class AppComponent implements OnInit {
  title = 'testing';
  ...
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Note that the AppComponent requires a CompanyService parameter. For now, we won't use it in the test though, so we just pass null.
* Karma should still be running from your last test and on save of the spec file automatically re-run.

