<p align="center"><img src="https://i.imgur.com/b4uo72l.png" width="auto" height="75px" /><p/>

<p align="center">
<strong>Fast - Minimal - Easy</strong>
</p>

<p align="center">
http://zamjs.com
</p>

<p align="center"><img src="https://travis-ci.org/roecrew/zam.svg?branch=master" /> <a class="badge-align" href="https://www.codacy.com/app/roecrew/zam?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=roecrew/zam&amp;utm_campaign=Badge_Grade"><img src="https://api.codacy.com/project/badge/Grade/b47e18bf79834015842bf7e65ff7d565"/></a></p>

<p align="center">Interested in contributing?</p><p align="center">Click <a href="https://join.slack.com/t/zamjs/shared_invite/enQtMjk1OTIyMDgzMTUyLTkxNmJkMDBjM2ZkNDA5Y2EyMzk1NTM4OTg3Mzc3MmE0NjJlMWYzNTg3YjdhMmFjM2E4NTQzMWVmNjhhZThiNjU">here</a> to join the slack channel!</p>

## Overview

Zam is a component-based micro-library (about 3KBs).

Zam objects can be thought of as components. These components generate a specified structure of elements, which are mounted to the DOM.

By confining/compartmentalizing the DOM elements that make up a structure to a Zam component, we create a cleaner coding environment. Through the process of abstraction, a Zam component hides all but the relevant data — in order to reduce complexity and increase efficiency.

##

Basically Zam can build this.

<img src="https://i.imgur.com/zf4gIMp.png" width="auto" height="75px" />

By doing this.
```html
<uiswitch>
</uiswitch>
```
```javascript
UISwitch.render();
```

Instead of doing this...

```css
.ui-switch {
  position: relative;
  background-color: #d0d2d3;
  margin: 50px;
  padding: 10px;
  width: 60px;
  height: 20px;
  border: 1px solid clear;
  border-radius: 50px;
  text-align: right;
  transition: background-color 0.1s ease-out;
}

.ui-switch-circle {
  position: absolute;
  left: 5px;
  top: 5px;
  width: 30px;
  height: 30px;
  background-color: white;
  border: 1px solid clear;
  border-radius: 50px;
  box-shadow: 0 0 1px 0 rgba(0, 0, 0, 0.25), 0 4px 11px 0 rgba(0, 0, 0, 0.08),
    -1px 3px 3px 0 rgba(0, 0, 0, 0.14);
  transition: left 0.1s ease-out;
  cursor: pointer;
}

.ui-switch-text {
  position: absolute;
  background-color: initial;
  top: 11px;
  left: 45px;
  transition: left 0.1s ease-out;
}
```
```html
<div class="ui-switch">
    <span class="ui-switch-text">
        Off
    </span>
    <div class="ui-switch-circle">
    </div>
</div>
```
```javascript
var circles = document.querySelectorAll('.ui-switch-circle');
var len = circles.length;
for(var i=0; i<len; i++) {
  circles[i].addEventListener('click', function(e) {
    var circleStyle = e.target.style;
    circleStyle.left === '' ? circleStyle.left = '10px' : circleStyle.left = '';
    var switchStyle = e.target.parentNode.style;
    switchStyle.backgroundColor === '' ? switchStyle.backgroundColor = 'rgb(76, 218, 99)' : switchStyle.backgroundColor = '';
    var textStyle = e.target.parentNode.querySelectorAll('.ui-switch-text')[0].style;
    textStyle.left === '' ? textStyle.left = '45px' : textStyle.left = '';
    var textNode = e.target.parentNode.querySelectorAll('.ui-switch-text')[0];
    textNode.innerHTML === 'Off' ? textNode.innerHTML = 'On' : textNode.innerHTML = 'Off';
  });
}
```

## Import

### Current Stable Build is 10.4

```javascript
inport Zam from "https://cdn.jsdelivr.net/npm/zamjs@10.4.0/zam.min.js"
```
```
npm install zamjs@10.4.0
```

## Quickstart

Zam is component based.

<strong>Every Zam object represents and manages a single DOM Element.</strong>

Example - Hello World!

```html
<html>
<head>
</head>
<body>
    <foo>
    </foo>
    <script type="module">
        import Zam from "https://cdn.jsdelivr.net/npm/zamjs@10.4.0/zam.min.js";

        export class Foo extends Zam {
            constructor() {
                super();
                this.append(new Zam('<div>Hello {{someData}}!</div>'), 'hello-text');
                this.append(new Zam('<input type="text" z-bind="someData"></input>'), 'hello-input');
            }
        }
        
        Foo.render();
    </script>
</body>
</html>
```

In this case, instance 'root' manages DOM Element...

```html
<div>Hello World!</div>
```

##

Now we will expand on the Hello World Example, and utilyze the shadow DOM and introduce shadowRender().

```html
<html>
<head>
</head>
<body>
    <foo>
    </foo>
    <script type="module">
        import Zam from "https://cdn.jsdelivr.net/npm/zamjs@10.4.0/zam.min.js";

        export class Root extends Zam {
            constructor() {
                super();
                this.append(new Zam(`<div style="{{helloStyle}}">Hello {{someData}}!</div>`), 'hello-world1');
                this.append(new Zam(`<input z-bind="someData" placeholder="{{placeHolder}}" />`), 'input');
                this['hello-world1'].prop('helloStyle', 'font-size:30px;');
            }
        }
        
        var rootObjects = Root.shadowRender();
        rootObjects[0]['input'].prop('placeHolder', 'Type something...');
        rootObjects[1]['hello-world1'].prop('someData', 'Universe');
    </script>
</body>
</html>
```

<p align="center"><img src="https://i.imgur.com/JGeezFD.png"/></p>

## Examples

http://zamjs.com/examples

## Instance Properties

* <strong>.e</strong>

  * This is a given component's actual DOMElement.

  *  Example: someComponent.e.className

## Class Methods

* <strong>SubClass.render()</strong>

  * Example: MyComponent.render(); it renders all <mycomponent> tags.
  
  * Returns: Nothing.
  
* <strong>SubClass.shadowRender()</strong>

  * Example: MyComponent.shadowRender(); it shadowRenders all <mycomponent> tags.
  
  * Returns: Nothing.

* <strong>Zam.on(events, selector, function)</strong>

  * Example: Zam.on('mouseover', 'someSelector', someFunction);
  
  * Returns: Nothing.

* <strong>Zam.off(events, selector, function)</strong>

  * Example: Zam.off('mouseover', 'someSelector', someFunction);

  * Returns: Nothing.

## Instance Methods

* <strong>.append(component, key)</strong>

  * Example: someComponent.append(new Zam(`<div>Hello World</div>`), 'hello-world');
  
  * Returns: Component that was appended.

* <strong>.prepend(component, key)</strong>

  * Example: someComponent.prepend(new Zam(`<div>Hello World</div>`), 'hello-world');
  
  * Returns: Component that was prepended.

* <strong>.replace(component, key)</strong>

  * Example: someComponent.replace(new Zam(`<div>Hello World</div>`), 'hello-world');
  
  * Returns: Component that replaced old component.

* <strong>.remove()</strong>

  * Example: someComponent.remove();
  
  * Returns: Nothing.

* <strong>.on(events, function)</strong>

  * Example: someComponent.on('mousedown', someFunction);
  
  * Returns: component that called .on().

* <strong>.off(events, function)</strong>

  * Example: someComponent.off('mousedown', someFunction);
  
  * Returns: component that called .off().
  
* <strong>.customEvent(event)</strong>

  * Example: someComponent.customEvent('some-event');
  
  * Returns: Nothing.
  
* <strong>.dispatchEvent(event)</strong>

  * Example: someComponent.dispatchEvent('some-event');
  
  * Returns: Nothing.