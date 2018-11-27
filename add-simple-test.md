# 5. Add simple test

* Delete the default tests made by the Angular CLI

\*\*src/app/app.component.spec.ts

* Add a `describe` block.

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
describe(`Component: App Component`, () => {

});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Add a `it` block.

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
describe(`Component: App Component`, () => {
  it('add 1+1 - PASS', () => {

  });
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Add an expectation.

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
describe(`Component: App Component`, () => {
  it('add 1+1 - PASS', () => {
        expect(1 + 1).toEqual(2);
  });
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Run the test with Karma test runner <a id="runthetestwithkarmatestrunner"></a>

* In the terminal at the path of the project start the unit tests with the following command

```text
ng test
```

![](https://firebootcamp.ghost.io/content/images/2017/02/2017-02-21_22-27-45.jpg)

**Figure: Karma output in terminal**



