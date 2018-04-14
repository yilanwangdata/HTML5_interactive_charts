# HTML5_interactive_charts
**Canvas**

KineticJS library

for more information: http://kineticjs.com/

**local storage**
```
localStorage.setItem('Item Name','Item Value')
localStorage.getItem('Item Name')
```
Use caniues.com under "File API"

**set initial stage**
```
<!DOCTYPE HTML>
<html>
	<head>
<title>TPA: Trans Planet Airlines - Lunar Leaper Training</title>
<link href="styles/main.css" rel="stylesheet" type="text/css">
	<script type="text/javascript" src="http://code.jquery.com/jquery-1.8.2.min.js"></script>
```
go to head section to link the javasript file
```
<script type="text/javascript" src="scripts/kinetic-v4.40.js"></script>
	<script type="text/javascript" src="scripts/canvas_chart.js"></script>
	</head>
	<body onmousedown="return false;">
<div id="outerWrapper">
  <div id="header"><img src="images/logo.png" width="410" height="181" alt="TPA: Trans Planet Airlines" /><br>
    <img src="images/tpa_name.gif" width="373" height="37" alt="Trans Planet Airlines"> </div>
  <div id="nav">
    <h1>Lunar Leaper Training</h1>
  </div>
  <div id="content">
    <div id="steps">
      <p>Chart your training progress by dragging the corner of the daily bars to the height you reached that day of the training. To make a momento of your training progress, click the Training Complete button.</p>
    </div>
 ```
 
put this div tag right below the step div of instructions
```
    <div id="container"></div>
    <div>
    	<button id="saveImage">Training Complete!</button>
    </div>
  </div>
  <div id="footer">
    <p>Copyright &copy; 2054 Trans Planet Airlines, LLC. All rights reserved</p>
  </div>
</div></body>
</html>
```



```
// Load source images
function loadImages(sources,callback){
	var images={};
	var loadedImages=0,
	var numImages=0,
	for(var scr in sources){
		images[scr]=new Image();
		images[scr].onload=function(){
			if(++loadedImages>=numImages){
				callback(images);
			}
		};
		images[scr].scr=sources[scr];
	}
}
```
first function to set up, use the Kinetic js syntax to create our stage and point it toward container div

the id of div  that's gona hold canvas tag
```
// Initialize stage
function initStage(images) {
	var stage = new Kinetic.Stage({
		container: 'container',
		width: 600,
		height: 400
	});
	var bgLayer= new Kinetic.Layer();
	//background images
	var bgImg=new Kinetic.Image({
		x:0,
		y:0,
		image:images.moonSurface,
		width:600,
		height:476,
		name:'image'
	});
	bgLayer.add(bgImg);
	stage.add(bgLayer);
	stage.draw();
} // End initStage()

// Update anchors if group moved

// Create anchor groups

// Set image sources
var sources={
  moonSurface:'images/plum_apollo16_big.jpg'
};
// Load images and initialize stage when done
loadImages{sources,initStage}

