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

#### knockout.drop-upload-bindings.js

A binding handler for a dropzone where you can drop files to upload.

Use it like this:

```css
/*css*/
.drop-zone {
    -moz-user-select: none;
    -webkit-user-select: none;
    -ms-user-select: none;
    user-select: none;
    -o-user-select: none;
    height: 250px;
    background-color: #eee;
    border: 1px solid #222;
    display: flex;
    justify-content: center;
    flex-direction: column;
    text-align: center;
}

    .drop-zone.enter-drag {
        border: 1px solid #078d13;
        background-color: #6ca984;        
    }
    
    .drop-zone.leave-drag {
    
    }
```

```html
<!--html-->
<label>Files:</label>
<div class="drop-zone" data-bind="dropUpload: files" unselectable="on" onselectstart="return false;" onmousedown="return false;">
  <label>Drag &amp; drop files or double click.</label>
</div>

<!-- ko if: files().length > 0 -->
<label>Files waiting to be uploaded</label>
<ul>
  <!-- ko foreach: files -->
  <li>
    <b data-bind="text: name"></b>
  </li>
  <!-- /ko -->
</ul>
<button type="button" data-bind="click: function() { upload(files); }">
  Upload!
</button>
<!-- /ko -->
```

```javascript
//javascript
function AppViewModel() {
  var self = this;

  self.files = ko.observableArray();
  self.progress = ko.observable();
  self.upload = function(files) {

    alert("Your files are going to be uploaded!");

    var formData = new FormData();

    files().forEach(function(file) {
      formData.append("files", file);
    });

    $.ajax({
        url: "../api/upload",
        type: "POST",
        contentType: false,
        data: formData,
        dataType: "json",
        cache: false,
        processData: false,
        async: false,
        xhr: function() {
          var xhr = new window.XMLHttpRequest();
          xhr.upload.addEventListener("progress",
            function(evt) {
              if (evt.lengthComputable) {
                var progress = Math.round((evt.loaded / evt.total) * 100);
                self.progress(progress);
              }
            },
            false);
          return xhr;
        }
      })
      .done(function(data, textStatus, jqXhr) {})
      .fail(function(jqXhr, textStatus, errorThrown) {})
      .always(function() {});
  }
}

ko.applyBindings(new AppViewModel());
```

