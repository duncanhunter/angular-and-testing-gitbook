# 6. Add simple failing test

* Add another test, this time with a failing assumption.

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.spec.ts" %}
```typescript
describe(`Component: App Component`, () => {
  it('add 1+1 - PASS', () => {
        expect(1 + 1).toEqual(2);
  });
  
  it('add 1+1 - FAIL', () => {
        expect(1 + 1).toEqual(42);
  });
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* run ng test again. This time, you should see one failure.



