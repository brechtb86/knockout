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

#### knockout.bootstrap-modal-bindings.js

A binding handler for Bootstrap's modal.

Use it like this:

```html
<!--html-->
<div id="myModal" class="modal fade" role="dialog" data-bind="modal: showModal">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal">&times;</button>
        <h4 class="modal-title">Knockout bootstrap modal</h4>
      </div>
      <div class="modal-body">
        <p>It works!</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
<button type="button" data-bind="click: function() { showModal(true); }">
Show the modal!
</button>
```

```javascript
//javascript
function AppViewModel() {
  var self = this;

  self.showModal = ko.observable(false);
  self.showModal.subscribe(function(newValue) {
    if (!newValue) {
      alert("You closed the modal");
    }
  });
}

ko.applyBindings(new AppViewModel());
```

See an example on [JSFiddle](https://jsfiddle.net/brechtb86/dnj1n1dg/3/)






