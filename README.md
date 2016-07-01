# TiandTa
Tilt-And-Tap JavaScript Plugin
=

Table of Contents
-
+ [Motivation](#motivation)
+ [Installation](#installation)
+ [The Two Dimensional Use Case](#the-two-dimensional-use-case) 
+ [Example Usage](#example-usage) 
+ [Options](https://github.com/lindig11/TiandTa/wiki/Options) 

## Motivation
The idea is to make it easier to develop motion-sensitive websites. By enhancing websites with motion gestures, we allow for new kinds of interactions and improved user experience. Obvious simple usages are scrolling in on dimension (instead of swiping), little browser games, and more.

## Installation
Include the script somewhere in your webpage. Within the **<head>** is recommended.

```javascript
<script src="/path/to/tiltandtap.js"></script>
```

## The Two Dimensional Use Case

The plugin can be used for an application that wants to move an object in two dimensions. We call that object **indicator**. Other static elements may be present. The indicator can trigger a callback by entering or leaving those elements. We call this use case **TwoDimensionalTilt**.

 
The setup looks as follows:

```javascript
var plugin = new TiltAndTap();

//TwoDimensionalTilt
plugin.TwoDimensionalTilt(indicatorClassName, container, moveType, tap, elements, onEnter_callback, onExit_callback);
```

#### Table explaining parameters

| **Parameter Name**     | **Description**                                                                                                              | **Type**                 |
|--------------------|--------------------------------------------------------------------------------------------------------------------------|----------------------|
| indicatorClassName | A string that defines the style of the indicator. Can also be of type dictionary.                                        | "string" or { ... }  |
| container| Container says where the indicator resides in.  | DOM-Object           |
| elements           | Array of elements that the indicator can interact with.                                               | Array of DOM-Objects |
| MoveType           | Specifies movement type and several options. Look at examples or Option page for details.                                | Object               |
| Tap                | Specifies if tilting is enabled at all times (null), on tap (true), or only active when not touching the screen (false). | Boolean or null.     |
| Callback           | Developer defined callback function. Executed upon overlap with one of the elements.                                       | Function                     |

## Example Usage

Used when an object should move within a specified (two dimensional) area. In the example, the movable object can interact with fix positioned elements. In the example, upon overlap that element turns green, on exit it turns yellow.

#### HTML
```html
<div id="container">
    <div id="elem1" class="elem"></div>
    ...
    <div id="elem_n" class="elem"></div>
</div>
```

#### JavaScript
```javascript
var plugin = new TiltAndTap();

var container = document.getElementById("container");
var elements = document.getElementsByClassName("elem");

var cssClassName = "movableObject";

var tap = false //continuous tap disables tilting gestures

var onEnter_callback = function(element) {
    element.style["background-color"] = "green";
};

var onExit_callback = function(element) {
    element.style["background-color"] = "yellow";
};

var moveType = 
    {
        name : 'constantMove', //a movement that doesn't accelerate
        settings : {
            moveData: {
                speed: 5 //in px per interval
            },
            zone: {
                type: 'angles',
                vertical: [-15,15],
                horizontal: [-20,20]
            }
        }
    };

plugin.TwoDimensionalTilt(cssClassName, container, moveType, tap, elements, onEnter_callback, onExit_callback);
```

### DEMO **TODO**
