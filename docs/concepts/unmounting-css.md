# Unmounting css
Most React css libraries never clean up the `<style>` elements from the DOM. Instead, more and more
css is appended to the dom as you load code and mount components.

One distinctive feature of Kremling is that it will only append your css to the DOM when necessary.
This means that before your components are mounted, there will not be any `<style>` elements
appended to the DOM.

Additionally, kremling will remove `<style>` elements from the DOM as soon as there are no more components
using a css string. This is beneficial for overall DOM performance, since the browser will not have to deal
with a continuously growing set of css rules that do not apply to anything currently in the dom.
