# Knockout extensions
#### knockout.subscribe-changed.js


A simple extension on subscribable to have the oldValue and newValue as parameters.

Use it like this:

```html
<!--html-->
<button type="button" data-bind="click: function() { name('Spock'); }">
Change my name!
</button>
```

```javascript
//javascript
function AppViewModel() {
  var self = this;

  self.name = ko.observable("Brecht");
  self.name.subscribeChanged(function(newValue, oldValue) {
    if (newValue != oldValue) {
      alert("Hi " + oldValue + ", you changed your name to " + newValue);
    }
  });
}

ko.applyBindings(new AppViewModel());
```

See an example on [JSFiddle](https://jsfiddle.net/brechtb86/37q806rf/)
