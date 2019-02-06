# Naming css classes
When writing css classes with kremling, you can choose however you would like to name your css classes.

Here are a few recommendations from the kremling team, but feel free to deviate in whatever way you'd like to:

## Camel case vs hyphens
```css
.myButton {} /* camel case */
.my-button {} /* hyphens */
```

You can use either camel case or hyphens when naming your css classes. Many css-in-js libs for React
will encourage you to name css classes with camel case so that they are easier to use in javascript. However, with
kremling it truly doesn't matter since you will never need to reference your css classes with javascript variables.

*Soft recommendation*: Use hyphens, since that's the de facto standard in html and css.

## Start with very simple names
With kremling, you don't have to worry about your css leaking out of its scope, which means you can
name your css class something generic like `.button {}` and not have to worry about it colliding with
dom elements in a completely different area of your app.

```css
/* easy for humans to understand, so start by naming things like this */
.big-button {}

/* might avoid some naming collisions, but only change to it if you need to */
.big-button-for-modal {}
```

## Ampersands (&)
If you are using [kremling-loader](/walkthrough/kremling-loader.md), you'll never have to insert ampersands into your css.

If you are not, you will have to add ampersands before every css rule.

### Examples
```css
/* if you're not using kremling-loader */

/* put an ampersand before your class name */
& .foo {}

/* put an ampersand before any other type of css rule */
& div {}

/* put an ampersand before each rule in a list of rules */
& .bar, & .baz, & .bing {}
```
