#CDVGamepad
----

So you want to add a gamepad to a html5/canvas based app in [cordova](http://cordova.apache.org/)

##Cordova
###The Basics
---

install cordova

```
[sudo] npm install -g cordova
```

navigate to the directory where you want to create your app

```
cd [directory]
```

create an app

```
cordova create [app-directory] [reverse domain-style identifier] [application display name] && cd [app-directory]
```

add CDVGamepad plugin https://github.com/32teeth/cordova-plugin-gamepad.git

```
cordova plugin add https://github.com/32teeth/cordova-plugin-gamepad.git
```

iOS9 long press fix (optional)

*this prevents the copy/select bubble from coming up in games where the user needs to press and hold)*

```
cordova plugin add cordova-plugin-ios-longpress-fix
```

Add some platforms

```
cordova platform add ios
cordova platform add android
cordova platform add amazon-fireos
cordova platform add blackberry10
cordova platform add firefoxos
```

Prepare your platforms

```
prepare platform add ios
prepare platform add android
prepare platform add amazon-fireos
prepare platform add blackberry10
prepare platform add firefoxos
```

###CDVGamepad setup and configurations
---
in you cordova index.js add *CDVGamepad.setup()*

```
/*
** this is a basic joystick and 1 button setup with start and select buttons
*/
onDeviceReady: function() {
	CDVGamepad.setup();
}
```
##Configuration options

*CDVGamepad is fully customizable, from button names, colors, layout and more.*

| property | type | value(s) | description | example |
|-|-|-|-|-|
|debug|boolean|true/false|show or hide event debug info, default is false|```debug:false```|
|trace|boolean|true/false|show or hide gamepad trace info, default is false|```trace:false```|
|canvas|string|id of target canvas|if left out, creates a new canvas object|```canvas:"game"```|
|buttons|array|[]|collection of button objects|```[{name:"x",color:"rgba(255,255,0,0.5)"}]```|
|button|object|{name:string,color:hex\|rgb\|rgba}|properties for custom buttons|```[{name:"x",color:"rgba(255,255,0,0.5)"},{name:"y",color:"rgba(255,0,255,0.5)"}]```|
|layout|string|TOP_LEFT \| TOP_RIGHT \| BOTTOM_LEFT \| BOTTOM_RIGHT|cardinal position of buttons default is BOTTOM_RIGHT|```layout:"BOTTOM_RIGHT"```|
|start|boolean|true/false|display start button, default is true|```start:false```|
|select|boolean|true/false|display select button, default is false|```select:false```|
|hidden|boolean|true/false|show or hide the gamepad, default is false, this can be used to hide the gamepad if you are doing something else on screen|```hidden:false```|

###Config examples
######*default options*

![default options](https://raw.githubusercontent.com/32teeth/cordova-plugin-gamepad/master/images/CDVGamepad-1.png)

```
CDVGamepad.setup();
```

######*one button, custom name, no start button*

![default options](https://raw.githubusercontent.com/32teeth/cordova-plugin-gamepad/master/images/CDVGamepad-2.png)

```
CDVGamepad.setup({
	start:false,
	buttons:[
		{name:"jump"}
	]
});
```

######*two buttons, custom names, custom colors, with select button*

![default options](https://raw.githubusercontent.com/32teeth/cordova-plugin-gamepad/master/images/CDVGamepad-3.png)

```
CDVGamepad.setup({
	select:true,
	buttons:[
		{name:"x",color:"rgba(255,255,0,0.5)"},
		{name:"y",color:"rgba(0,255,255,0.75)"}
	]
});
```

######*target canvas*

![default options](https://raw.githubusercontent.com/32teeth/cordova-plugin-gamepad/master/images/CDVGamepad-4.png)

```
CDVGamepad.setup({
	canvas:"game"
});
```

######*change layout canvas*

![default options](https://raw.githubusercontent.com/32teeth/cordova-plugin-gamepad/master/images/CDVGamepad-5.png)

```
CDVGamepad.setup({
	layout:"BOTTOM_LEFT"
});
```

######*show trace & debug info*


![default options](https://raw.githubusercontent.com/32teeth/cordova-plugin-gamepad/master/images/CDVGamepad-6.png)

```
CDVGamepad.setup({
	trace:true,
	debug:true
});
```

######*all out everything*


![default options](https://raw.githubusercontent.com/32teeth/cordova-plugin-gamepad/master/images/CDVGamepad-7.png)

```
CDVGamepad.setup({
	select:true,
	trace:true,
	debug:true,
	canvas:"game",
	buttons:[
		{name:"z", color:"#17861c"},
		{name:"y", color:"rgb(134, 83, 23)"},
		{name:"x", color:"rgba(204, 0, 51, 0.5)"},		
	]
});
```

######*hidden gamepad*

![default options](https://raw.githubusercontent.com/32teeth/cordova-plugin-gamepad/master/images/CDVGamepad-8.png)

```
CDVGamepad.setup({
	hidden:true
});
```

###CDVGamepad observable method
---
CDVGamepad has an observable method that returns the current state map of the gamepad

**observe();**

```
CDVGamepad.setup()
/*
** the below example simply logs out the observe method return
*/
setInterval(
	function()
	{
		var map = CDVGamepad.observe();
		console.log(new Date() + ":" + JSON.stringify(map))
	}
	,1000
);
```