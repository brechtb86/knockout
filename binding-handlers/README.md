# Knockout binding handlers
#### knockout.highlight-bindings.js


A simple binding handler to highlight words in a text based on keywords.

Use it like this:

```css
/*css*/
span.high-lighted{
	background-color: #FFFF00;
}
```

```html
<!--html-->
<html>
<body>
	<p data-bind="highlight: { text:  text(), keywords: keywords() }">
</body>
</html>
```

```javascript
//javascript
function AppViewModel() {
    var self = this;
 
    self.keywords = ko.observableArray([
	"highlight",
	"text"
    ]);
 
    self.text = ko.observable("The keywords in this text are highlighted.");
}
 
ko.applyBindings(new AppViewModel());

```

See an example on [JSFiddle](https://jsfiddle.net/brechtb86/jskjdhqv/)
