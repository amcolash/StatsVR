# StatsVR
FPS, MS and Custom Values HUD specifically for WebVR &amp; THREE.js Projects that use a HMD, such as Oculus Rift

The StatsVR view displays inside the HMD as a HUD, always facing the camera, and always on top.

## Video Tutorial of using StatsVR
[![StatsVR Tutorial for WebVR and ThreeJS projects](https://img.youtube.com/vi/TZNZoaiTUwg/0.jpg)](https://www.youtube.com/watch?v=TZNZoaiTUwg)

## Demo webpage showing example usage, 
https://sean-bradley.github.io/StatsVR-Demo/ (requires firefox, Oculus CV1, 2 Oculus Touch controllers and Rift Core 2.0 disabled in settings)


## Initial Setup

Download statsvr.min.js, save it, and include reference to script in your html head. eg

``<script type="text/javascript" src="statsvr.min.js"></script>``

Create global variables
```
var camera, scene, renderer;  // these are commonly used THREE.js variables and may already exist in your project
var statsVR; // create your global statsvr variable. I named mine statsVR

function init(){
	// existing THREE.js and webvr setup goes here
	// then after you've instantiated the THREE.js renderer, scene and camera objects,
	statsVR = new StatsVR(scene, camera);  // pass your scene and camera objects to the StatsVR constructor
}
init();
```

## Showing the Default FPS Counter and Graph
![Default FPS Counter and Graph](https://github.com/Sean-Bradley/StatsVR-Demo/blob/master/statsVR_FPS.jpg)

To show the default StatsVR FPS counter and graph, add the line 
``statsVR.update();`` 
anywhere inside your THREE.js render or animation loop.

eg,
```
function render() {
	// your existing animation magic

	statsVR.update();  // required anywhere within the loop

	renderer.render(scene, camera)
}
renderer.animate(render);
```

## Showing the FPS and also the optional MS Counters and Graphs
![FPS and Optional MS Counters and Graphs](https://github.com/Sean-Bradley/StatsVR-Demo/blob/master/statsVR_FPS_MS.jpg)

To show the StatsVR FPS along with the optional MS counter and graph, also add the lines

```
statsVR.msStart();
//code you want to monitor the MS duration of goes here
statsVR.msEnd();
``` 

anywhere inside your THREE.js render or animation loop.

eg,
```
function render() {
	// your existing animation magic
	statsVR.msStart(); // starts the MS monitor timespan
	// specific code you want to monitor the MS duration of goes here
	statsVR.msEnd(); // ends the MS monitor timespan
	
	statsVR.update(); //required anywhere within the loop

	renderer.render(scene, camera)
}
renderer.animate(render);
```
or, if you want to check the MS duration of your entire render or animation loop, put the ``msStart()`` and ``msEnd()`` procedure calls at the beginning and end of your entire render loop.
eg,
```
function render() {
	statsVR.msStart(); // starts the MS monitor timespan

	// your existing animation magic
	
	statsVR.update();  // required anywhere within the loop

	renderer.render(scene, camera)
	
	statsVR.msEnd(); // end the MS monitor timespan
}
renderer.animate(render);
```


### Also Show the optional custom fields along with the usual FPS and optional MS Counters and Graphs.
![FPS, MS and Custom fields](https://github.com/Sean-Bradley/StatsVR-Demo/blob/master/statsVR_FPS_MS_3Customs.jpg)

You can also show up to 3 extra custom values in the display, such as values you may want to track during execution of your program.
eg, anywhere witihn your render loop,
```
statsVR.setCustom1(myVar);
statsVR.setCustom2(anotherVar);
statsVR.setCustom3(optionalyAnyOtherVarYouWantToMonitor);
```


### Customising the StatsVR position inside the HMD view
The default panel is shown at offset
```
X = 0,
Y = 1.5,
Z = -5 
```
from the camera position and rotation in the THREE.js worldspace.
You can modify those defaults if you want, eg, after you initialise the StatsVR object, you can change it's display coordinates.
```
statsVR.setX(1);
statsVR.setY(0);
statsVR.setZ(-10);
```


The benefit of using StatsVR is that you don't need to remove the HMD to view the FPS or any other custom variable you want to monitor.




