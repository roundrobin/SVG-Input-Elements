SVG Input Elements
==================

Currently this project implements text areas, similar in behaviour to HTML 
`<textarea>` tags. The goal is to implement input elements that feel and 
behave naturally (i.e. as corresponding HTML input elements etc). 

For a demo of the 0.2 release go to 
[josf.se/svg-input-elements/](http://josf.se/svg-input-elements/). You can 
also download the latest examples and test yourself, just change the path 
"../tools/build.js" to "../jquery.svg.input.js" unless you're on an Apache 
server with PHP. _Note:_ In Chrome the script will fail if you run it from 
your local file system 
[because of a bug](http://code.google.com/p/chromium/issues/detail?id=49001). 

(The generated files in the root might not always be 100% up to date.) 

This project started out as a sub-project to a master thesis project, 
[Personas in Real Life](http://personasinreallife.tumblr.com).

__Go to:__ [Features](#features-), [Requirements](#requirements), 
[Getting Started](#getting-started), [Events](#events), [Versions](#versions) 
or [Development](#development)

Features 
--------
* Line wrapping
* Word wrapping of long words
* Copy/cut/paste
* Text selection with mouse and keyboard
* Change cursor position with left/right/up/down/home/end etc
* Handles both paragraphs (_enter_) and manual line breaks (_shift+enter_)
* Undo/redo
* ...

Requirements
------------
This project requires [jQuery](http://docs.jquery.com/Downloading_jQuery) 
(we're using 1.7.2) and the 
[jQuery SVG plugin](http://keith-wood.name/svg.html)

Getting Started
---------------
[Download jQuery](http://jquery.com/) (we've tested on version 1.7.2) and 
[jQuery SVG](http://keith-wood.name/svg.html) (tested on version 1.4.5) and 
include these libraries, and SVG Input Elements: 
```
<script type="text/javascript" src="jquery.js" />
<script type="text/javascript" src="jquery.svg.js" />
<script type="text/javascript" src="jquery.svg.input.js" />
```
Also include some styles (apologies for bad documentation and coding on this 
part, SVG Input Elements doesn't behave as expected if certain styles aren't 
defined. Also, in a futur version all SVG Input Elements classes and IDs will 
have a special prefix.):
```
<link rel="stylesheet" href="svg.css" />
```
Create an inline SVG element with the following attributes (the ID is optional
but useful, especially if you have more than one SVG element): 
```
<svg id="svg" version="1.1" xmlns="http://www.w3.org/2000/svg" xlink="http://www.w3.org/1999/xlink" unselectable="on" style="-webkit-user-select: none;"></svg>
```
Make sure that the document is loaded before we start manipulating it, see the
[jQuery SVG documentation](http://keith-wood.name/svgRef.html) for more 
information on this: 
```
$(document).ready(function(){
  $('#svg').svg({onLoad: init, settings: {}});  
});
```

You can now create a textarea using the following code: 
```
function init(svg) {
    var parent = $('#svg')[0]; 
    var x = 10; 
    var y = 10; 
    var settings = {width: '200'}; 

    var textArea = svg.input.textArea(parent, x, y, "text", settings);
}
```
the `parent` parameter is optional. The properties of the `settings` object 
corresponds to the attributes of an SVG `<g>` tag, plus an additional `width` 
parameter. 
 
You should now have a working text area!

###Binding Events
SVG Input Elements trigger events that you can bind: 
```
textArea.bind("change", function(e, text) {
  alert("text changed: " + text);
}
textArea.bind("changeSize", function(e, height, width) {
  alert("dimensions changed: " + height + "x" + width);
}
```

Events
------
change: Triggered when the SVG Input Element has changed in some way, i.e. for
a textbox it is triggered every time a character is removed or added. Returns 
one parameter: 
  * _param1_: The new text
changeSize: Triggered when the size of the SVG Input Element changes. Returns 
two parameters: 
  * _param1_: The new width
  * _param2_: The new height

Versions
--------
###v1.0
__Scheduled early June.__ This release will provide several text related input
elements and should be stable on all major browsers except perhaps for 
Internet Explorer, which seems to have very poor SVG support even in verion 9. 

###v0.3
__Coming soon.__ Will feature a list variant of the text input element. 

###v0.2.2
__Released 30 May 2012.__ Minor enhancements, bugfixes and useable events. 

###v0.2.1
__Released 16 May 2012.__ Minor enhancements, bugfixes and support for 
@import. No longer requires support for the xml:space attribute. 

###v0.2
__Released 15 May 2012.__ This release provides bugfixes and several 
improvements and should also work on Firefox. Additional input elements are 
postponed to the next release. The documentation is still lacking, contact us 
if you want help. 

###v0.1
__Released 9 May 2012.__ This is a rather limited release which is only 
properly tested in Chrome/Chromium. It should not be seen as something that is
ready to be put in use.

Development
-----------
Next in line to be implemented are variations of the text area (like a list 
box, for example) and an image input element. 

Feel free to join in and develop, if you want to contact us please e-mail 
Tim at [info@sypreme.se](mailto:info@sypreme.se) or Josef at 
[josef.ottosson@josf.se](mailto:josef.ottosson@josf.se). 

In a future version, we would build it both for JQuery SVG and Raphael, or 
rid of both dependencies completely. We would love some help implementing 
this! About choosing which to build for, we refer to this thread (for now):
http://stackoverflow.com/questions/588718/jquery-svg-vs-raphael