# [Canvas Designer](https://github.com/muaz-khan/Canvas-Designer) / [LIVE Demo](https://www.webrtc-experiment.com/Canvas-Designer/) - [API Referencee](https://github.com/muaz-khan/Canvas-Designer#api-reference)

> "Collaborative" [Canvas Designer](https://github.com/muaz-khan/Canvas-Designer) i.e. Canvas-Drawing tool allows you draw bezier/quadratic curves, rectangles, circles and lines. You can also set strokes, back/forth colors and much more. You can draw using pencils, erase drawing, type texts etc. You can [easily add your own tools](https://www.webrtc-experiment.com/Canvas-Designer/Help/#contribute).

This specialty of this drawing-tool is that, it generates Canvas2D code for you; so simply draw and get the code! That code can be used in any javascript Canvas2D application.

Also, you can collaborate your drawing with up to 15 users; and everything is synced from all users. So, if you draw a line and your friend-A draws quadratic curve and friend-B draws rectangle then everything will be synced among all users!

# [Click to view Gif Presentation](https://cdn.webrtc-experiment.com/images/Canvas-Designer.gif)

<img src="https://i.imgur.com/uDbfy1F.png" />

# Built-in tools

You can use [`CanvasDesigner.setSelected`](https://github.com/muaz-khan/Canvas-Designer#setselected) or [`CanvasDesigner.setTools`](https://github.com/muaz-khan/Canvas-Designer#settools) for below tools.

1. `line` --- to draw straight lines
2. `pencil` --- to write/draw shapes
3. `dragSingle` --- to drag/move last shape
4. `dragMultiple` --- to drag/move all shapes
5. `eraser` --- to erase/clear specific portion of shapes
6. `rectangle` --- to draw rectangles
7. `arc` --- to draw circles
8. `bezier` --- to draw bezier curves
9. `quadratic` --- to draw quadratic curves
10. `text` --- to write texts
11. `image` --- add external images

# Features

1. Draw single or multiple shapes of any kind (according to toolbox)
2. Drag/resize/adjust all the shapes in any possible direction
3. Rectangles and images can be resized in 4-directions

   Red transparent small circles helps you understand how to resize.

4. Undo drawings using `ctrl+z` keys
5. Drag/move single or all the shapes without affecting any single coordinate

# How to Use

<ol>
    <li>Take all code from <a href="https://github.com/muaz-khan/Canvas-Designer">this link</a> and upload somewhere on your site.</li>
    <li>Target directly will be having this file: <a href="https://github.com/muaz-khan/Canvas-Designer/blob/master/canvas-designer-widget.js">canvas-designer-widget.js</a>. Link this file in your HTML/PHP page.</li>
    <li>
        Use this command to append widget in your HTML page:<br>
            
        <code>CanvasDesigner.appendTo(document.documentElement);</code>
    </li>
</ol>

# Complete Usage

```javascript
websocket.onmessage = function(event) {
    CanvasDesigner.syncData( JSON.parse(event.data) );
};

CanvasDesigner.addSyncListener(function(data) {
    websocket.send(JSON.stringify(data));
});

CanvasDesigner.setSelected('pencil');

CanvasDesigner.setTools({
    pencil: true,
    text: true
});

CanvasDesigner.appendTo(document.documentElement);
```

It is having `CanvasDesigner.destroy()` method as well.

# Use [WebRTC](http://www.rtcmulticonnection.org/docs/)!

```javascript
webrtc.onmessage = function(event) {
    CanvasDesigner.syncData( event.data );
};

CanvasDesigner.addSyncListener(function(data) {
    webrtc.send(data);
});
```

# Use Socket.io

```javascript
socket.on('message', function(data) {
    CanvasDesigner.syncData( data );
});

CanvasDesigner.addSyncListener(function(data) {
    socket.emit('message', data);
});
```

# API Reference

## `syncData`

Pass array-of-points that are shared by remote users using socket.io or websockets or XMPP or WebRTC.

```javascript
CanvasDesigner.syncData(arrayOfPoints);
```

## `addSyncListener`

This callback is invoked as soon as something new is drawn. An array-of-points is passed over this function. That array MUST be shared with remote users for collaboration.

```javascript
CanvasDesigner.addSyncListener(function(data) {
    websocket.send(JSON.stringify(data));
});
```

## `setSelected`

This method allows you problematically select specific tools.

* See list of [all tools](https://github.com/muaz-khan/Canvas-Designer#built-in-tools)

```javascript
CanvasDesigner.setSelected('rectangle');
```

## `setTools`

This method allows you choose between tools that **should be displayed** in the tools-panel.

* See list of [all tools](https://github.com/muaz-khan/Canvas-Designer#built-in-tools)

```javascript
CanvasDesigner.setTools({
    pencil: true,
    text: true
});
```

## `appendTo`

CanvasDesigner is a widget; that widget should be appended to a DOM object. This method allows you pass `<body>` or any other HTMLDOMElement.

```javascript
CanvasDesigner.appendTo(document.body || document.documentElement);
```

## `destroy`

If you want to remove the widget from your HTMLDOMElement.

```javascript
CanvasDesigner.destroy();
```

## `toDataURL`

Get data-URL of your drawings! 

```javascript
CanvasDesigner.toDataURL('image/png', function(dataURL) {
    window.open(dataURL);
});
```

## `sync`

You can manually sync drawings by invoking `CanvasDesigner.sync` method:

```javascript
CanvasDesigner.sync();
```

Here is a real usecase:

```javascript
webrtcDataChannel.onopen = function() {
    if(CanvasDesigner.pointsLength > 0) {
        // you seems having data to be synced with new user!
        CanvasDesigner.sync();
    }
};
```

## `pointsLength`

Each shape is considered as a `point`. This value allows you check number of shapes that are already drawn on the canvas-designer.

```javascript
(function looper() {
    document.getElementById('number-of-shapes').inenrHTML = CanvasDesigner.pointsLength;
    setTimeout(looper, 1000);
})();
```

Or a real usage:

```javascript
websocket.onopen = function() {
    if(CanvasDesigner.pointsLength > 0) {
        // you seems having data to be synced with existing users!
        CanvasDesigner.sync();
    }
};
```

# How to contribute?

It is not too much complex to add new tools :) Its easy.

* https://www.webrtc-experiment.com/Canvas-Designer/Help/#contribute

# Demos

A-to-zee all shapes, and animations on following page is created using canvas-designer:

* http://muaz-khan.github.io/Everything/Canvas/
* https://www.webrtc-experiment.com/Canvas-Designer/ (canvas-designer demo allows you draw shapes & get the code; additionally collaborate as well!)
* Try a simple canvas2d animation demo: http://muaz-khan.github.io/Everything/Canvas/Experiments/Simple-HTML5-Canvas-Experiment/
* Try many other canvas2d demos: http://muaz-khan.github.io/Everything/Canvas/Experiments/

All above demos are built using canvas-designer!

Original source-code was shared 2-years back, here: https://github.com/muaz-khan/Everything/tree/gh-pages/Canvas/Tools/Designer

There is a similar "tinny" tool, however it isn't yet supporting collaboration: https://canvature.appspot.com/

And WebRTC-Experiments! https://github.com/muaz-khan/WebRTC-Experiment

# License

[Canvas Designer](https://github.com/muaz-khan/Canvas-Designer) is released under [MIT licence](https://www.webrtc-experiment.com/licence/) . Copyright (c) [Muaz Khan](http://www.MuazKhan.com).
