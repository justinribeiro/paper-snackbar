# \<paper-snackbar\>

Providing brief feedback about an operation through a message at the bottom of the screen that is loosely based on the [Material Design spec](https://material.io/guidelines/components/snackbars-toasts.html#).

## Usage

`<paper-snackbar>` sits at the top level of your application and listens for a custom event called `paper-snackbar-notify`. The basic steps for using it are:

1. Find a nice place to put it in your application. I usually choose my top level app element.

2. Call `paper-snackbar-notify` via `this.dispatchEvent(new CustomEvent('paper-snackbar-notify', ...));`.

3. Yipee, snackbar shows up!

## Demo

<!---
```
<custom-element-demo>
  <template>
    <script src="../webcomponentsjs/webcomponents-lite.js"></script>
    <link rel="import" href="paper-snackbar.html">
    <next-code-block></next-code-block>
  </template>
</custom-element-demo>
```
-->
```html
<style is="custom-style">
  paper-snackbar {
    --paper-snackbar-background:     #323232;
    --paper-snackbar-text:           #ffffff;
    --paper-snackbar-link:           #f4cb1e;
  }
</style>
<p>Clicking the button below will trigger the <code>paper-snackbar</code>.</p>
<button onclick="test()">Click Me!</button>
<br><br><br>
<script>
  function test() {
    
    document.dispatchEvent(new CustomEvent('paper-snackbar-notify', {
        bubbles: true, 
        composed: true,
        detail: { 
          message: 'Hi! I am a paper-snackbar!', 
          targetTitle: 'Link',
          targetUrl: '#'
        }
    }));

  }
</script>
```

## Styling

The following custom properties and mixins are available for styling:

| Custom property | Description | Default |
| --- | --- | --- |
| `--paper-snackbar-background` | Background color to entire element | `#323232` |
| `--paper-snackbar-text` | Color applied to element text | `#ffffff` |
| `--paper-snackbar-link` | Color applied to link element text | `#f4cb1e` |

## Using the mixin

Presuming you have a lot of forms or elements that just want to send snackbar messages all day long, you can also use the class mixin.

1. Import `paper-snackbar-mixin.html` into your element:
  ```html
  <link rel="import" href="../bower_components/paper-snackbar/paper-snackbar.html">
  ```
2. Extend from PaperSnackbarNotify():
  ```javascript
  class MyMagicalElement extends PaperSnackbarNotify(Polymer.Element) {}
  ```
3. When you want to use the snackbar, just call `this.paperSnackbarNotify()`:
  ```javascript
  this.paperSnackbarNotify('Your record was added.', 'view', '/some/link/you/want');
  ```

## Why?

This is largely based on what was in the Polymer SHOP demo. Then I decided I wanted this more global thing I could just call when shuffling forms in and out, so it got a little API. The it was because I keep recreating this and over again in various ways and I'm really tired of copy and paste.