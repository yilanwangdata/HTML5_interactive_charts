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
in html file
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

in canvas_chart.js file

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


create a new canvas image object for each element in the sources array, using the name and src attr

after all image has been looped through, call initStage function and pass the image array, create image object for each one of those
```
// Load source images
function loadImages(sources,callback){
	var images={};
	var loadedImages=0;
	var numImages=0;
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

add the argument:image

then populating the stage
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
```
Load the image so it can be used by canvas, which can load any number of image

First, define a var for image sources, can load multiple image if need
```
// Set image sources
var sources={
  moonSurface:'images/plum_apollo16_big.jpg'
};
// Load images and initialize stage when done
loadImages(sources,initStage);
```
loadimages: path--image name and source//callback function:what happened next after the image loaded

**add legend area and labels**
```
// Load source images
function loadImages(sources, callback) {
	var images = {};
	var loadedImages = 0;
	var numImages = 0;
	for(var src in sources) {
		images[src] = new Image();
		images[src].onload = function() {
		if(++loadedImages >= numImages) {
			callback(images);
		}
	  };
	  images[src].src = sources[src];
	}
}

// Initialize stage
function initStage(images) {
	var stage = new Kinetic.Stage({
		container: 'container',
		width: 600,
		height: 400
	});
```
we add something new here
```
	var legendArea = new Kinetic.Rect({
		x: 0,
		y: stage.getHeight() - 20,
		height: 20,
		width: stage.getWidth(),
		fill: 'white'
	});
	
	var dayOneLabel = new Kinetic.Text({
		text: 'Day 1',
		fontSize: 12,
		x: 40,
		y: stage.getHeight() - 18,
		fontFamily: 'sans-serif',
		fill: '#333333'
	});
	
	var dayTwoLabel = new Kinetic.Text({
		text: 'Day 2',
		fontSize: 12,
		x: 170,
		y: stage.getHeight() - 18,
		fontFamily: 'sans-serif',
		fill: '#333333'
	});
	
	var dayThreeLabel = new Kinetic.Text({
		text: 'Day 3',
		fontSize: 12,
		x: 300,
		y: stage.getHeight() - 18,
		fontFamily: 'sans-serif',
		fill: '#333333'
	});
		
	var layer = new Kinetic.Layer();
	var bgLayer = new Kinetic.Layer();

	// Background image
	var bgImg = new Kinetic.Image({
		x: 0,
		y: 0,
		image: images.moonSurface,
		width: 600,
		height: 476,
		name: "image"
	});
	

	bgLayer.add(bgImg);
	layer.add(legendArea);
	layer.add(dayOneLabel);
	layer.add(dayTwoLabel);
	layer.add(dayThreeLabel);
	stage.add(bgLayer);
	stage.add(layer);

	stage.draw();
```
```
} // End initStage()

// Update anchors if group moved

// Create anchor groups

// Set image sources
var sources = {
	moonSurface: 'images/plum_apollo16_big.jpg'
};

// Load images and initialize stage when done
loadImages(sources, initStage);
```
**draw bars and create bar group**
```
// Load source images
function loadImages(sources, callback) {
	var images = {};
	var loadedImages = 0;
	var numImages = 0;
	for(var src in sources) {
		images[src] = new Image();
		images[src].onload = function() {
		if(++loadedImages >= numImages) {
			callback(images);
		}
	  };
	  images[src].src = sources[src];
	}
}

// Initialize stage
function initStage(images) {
	var stage = new Kinetic.Stage({
		container: 'container',
		width: 600,
		height: 400
	});
```
this is new
```
	var dayOneBar = new Kinetic.Rect({
		x: 0,
		y: 0,
		width: 100,
		height: 10,
		name: 'bar',
		fill: '#B20000'
	});

	var dayTwoBar = new Kinetic.Rect({
		x: 0,
		y: 0,
		width: 100,
		height: 10,
		name: 'bar',
		fill: 'green'
	});

	var dayThreeBar = new Kinetic.Rect({
		x: 0,
		y: 0,
		width: 100,
		height: 10,
		name: 'bar',
		fill: 'blue'
	});
	var barOneY=370;
	var barTwoY=370;
	var barThreeY=370;

	var barOneGroup= new Kinetic.Group({
		x:10,
		y:barOneY,
		draggable:false
	});

	var barTwoGroup= new Kinetic.Group({
		x:140,
		y:barTwoY,
		draggable:false
	});

	var barThreeGroup= new Kinetic.Group({
		x:270,
		y:barThreeY,
		draggable:false
	});
```
```
	var legendArea = new Kinetic.Rect({
		x: 0,
		y: stage.getHeight() - 20,
		height: 20,
		width: stage.getWidth(),
		fill: 'white'
	});

	var dayOneLabel = new Kinetic.Text({
		text: 'Day 1',
		fontSize: 12,
		x: 40,
		y: stage.getHeight() - 18,
		fontFamily: 'sans-serif',
		fill: '#333333'
	});

	var dayTwoLabel = new Kinetic.Text({
		text: 'Day 2',
		fontSize: 12,
		x: 170,
		y: stage.getHeight() - 18,
		fontFamily: 'sans-serif',
		fill: '#333333'
	});

	var dayThreeLabel = new Kinetic.Text({
		text: 'Day 3',
		fontSize: 12,
		x: 300,
		y: stage.getHeight() - 18,
		fontFamily: 'sans-serif',
		fill: '#333333'
	});

	var layer = new Kinetic.Layer();
	var bgLayer = new Kinetic.Layer();

	// Background image
	var bgImg = new Kinetic.Image({
		x: 0,
		y: 0,
		image: images.moonSurface,
		width: 600,
		height: 476,
		name: "image"
	});


	bgLayer.add(bgImg);
	
	
        
```
put between this two, so that on top of the background but behind the legend
```
        layer.add(barOneGroup);
	layer.add(barTwoGroup);
	layer.add(barThreeGroup);
```
```
	layer.add(legendArea);
	layer.add(dayOneLabel);
	layer.add(dayTwoLabel);
	layer.add(dayThreeLabel);
	stage.add(bgLayer);
	stage.add(layer);
```
add each bar to its group
```
	barOneGroup.add(dayOneBar);

	barTwoGroup.add(dayTwoBar);

	barThreeGroup.add(dayThreeBar);


	stage.draw();

} // End initStage()

// Update anchors if group moved

// Create anchor groups

// Set image sources
var sources = {
	moonSurface: 'images/plum_apollo16_big.jpg'
};

// Load images and initialize stage when done
loadImages(sources, initStage);
```
