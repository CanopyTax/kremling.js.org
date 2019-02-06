# Scoped css
In Kremling, scoped css refers to css rules that only apply to a dom element container and all of its dom element children.

This is different from global css, where css classes can be used by any code in any place.

Scoped css is also different from local css, where css rules that only apply to the dom elements in a particular react component.

## Why scoped css?
Scoped css let's us not have to worry about global css class collision while also allowing us to inherit css from parent components
to child components if we want to. In that way, it does not try to prevent css cascading altogether, but instead allows you
pick and choose where in the dom you want your css rules to cascade.

Additionally, kremling's implementation of scoped css keeps your dom elements easy to understand at a glance, since there
is no need to generate unique class names for css rule.

## How to use it?
[useCss hook](/api/use-css.md)

[Scoped component](/api/scoped-component.md)

## How does this work under the hood?
Scoped css is accomplished by changing css rules to only apply when specific dom attributes are present. Normally,
css classes and rules are global, but when we change them to be scoped, you can have two css classes with the same name
that will apply to different parts of the dom.

Consider this HTML/CSS example, where two buttons have the same css class, but the first button is red and the second button is blue.
[Codepen example](https://codepen.io/joeldenning/pen/PVOzXK?editors=1100)

```html
<!-- index.html -->
<div kremling="0">
  <button class="my-button">First button</button>
</div>

<div kremling="1">
  <button class="my-button">Second button</button>
</div>
```

```css
/* styles.css */
[kremling="0"] .my-button {
  background-color: red;
  color: white;
}

[kremling="1"] .my-button {
  background-color: blue;
  color: white;
}
```

## Previous work
Scoped css is not an idea invented by the authors of Kremling. The [Svelte](https://svelte.technology/) framework, along with a variety
of other css libraries, already use this.
