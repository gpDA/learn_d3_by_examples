### What does it do
- Loading data into the browser's memory
- Binding data to elements within the document, creating new elements as needed
- Transforming those elements by interpreting each element's bound datum and setting its visual properties accordingly
- Transitioning elements between states in response to user input

### Alternatives
#### Easy Charts
Data Wrapper
Flot
Google Chart Tools
Highcharts
Peity
Timeline.js

#### Graph Visualizations
Arbor.js
Cytoscape.js
Sigma.js

#### Geomapping
Kartograph
Leaflet
Modest Maps
Polymaps

#### programming from scratch
p5.js
Paper.js
Raphael
Snap.svg
Two.js

#### Three-Dimensional
==> D3 is not the best at a 3D, simply because web browsers are historically two-dimensional beasts. 
But with increased support for WebGL, there are now more opportunities for 3D web experiences 
PhiloGL
Three.js

#### Tools Built with D3
==> General
Britecharts
C3.js
NVD3

==> Specialized
Crossfilter
 : usefuul for trying to squeeze your "big data" into a relatively small web browser
dc.js
 : The "dc" is short for dimensional charting, optimized for exploring large, multidimensional datasets
Firespray
 : Super-fast charting library for streaming data (Think high-density real-time data dashboards)

### CSS Rules
1) Selector matches cascade from the top down
Many style properties are inherited by an element's descendants unless otherwise specified.


```html
<style>
div {
    background-color: red;
    font-size: 24px;
    font-weight: bold;
    color: white;
}
</style>

<body>
    <p> I am a sibling to the div.</p>
    <div>
        <p>I am a descendant and child of the div. </p>
    </div>
</body>
```
The styles intended for the `div` are inherited by the second paragraph because that p is a descendant of the styled div

2) Moreover, when more than one selector applies to an element, the later rule generally overrides the earlier one
```css
p {
    color: blue;
}

p.highlight {
    color: black;
    background-color: yellow;
}
```
`p.highlight` selector would override the `p` rule even if it were listed first, simply because it is a more specific selector

3) If two selectors have the same specificity, then the later one will be applied

### JavaScript variable
#### 1) Arrays
 an array is a sequence of values, conveniently stored in a single variable
 keeping track of related values in separate variables is inefficient
 ```javascript
const numberA = 5;
const numberB = 10;
const numberC = 15;
const numberD = 20;
const numberA = 5;25
```

Rewritten as an array, those values are much simpler. Hard brackets [] indicate an array, and each value is separated by a comma
```javascript
const numbers = [5, 10, 15, 20, 25];
```

Very useful in data visualization, so you will becoome very comfortable with them. You can access a value in an array by using braket notation
```javascript
numbers[2] // returns 15
```

#### 2) Objects
Arrays are great for simple lists of values, but with more complex datasets, you will want to put your data into an object.
We include properties and values. A colon : separates each property and its value, and a comma separates each property / value pair
```javascript
const fruit = {
    kind: "grape",
    color: "red",
    quantity: 12,
    tasty: true,
};
```

To reference each value, we use dot notation, specifying the name of the property
```javascript
fruit.kind // returns "grape"
// ...
fruit.tasky // returns true
```

#### 3) Objects and Arrays
You can combine these two structures to create arrays of objects, or objects of arrays
We use hard brackets [] on the outside, to indicate an array, followed by curly brackets {} and object notation on the inside, with each object separated by a comma
```javascript
const fruits = [
    {
        kind: "grape",
        color: 'red',
        quantity: 12,
        tasty: true
    },
    {
        kind: "kiwi",
        color: 'brown',
        quantity: 98,
        tasty: true
    },
]
```

How to access every value in the fruits array of objects
```javascript
fruits[0].kind // 'grape'
fruits[0].color // 'red'
fruits[0].quantity // 12
fruits[0].tasty // true
```

#### 4) JSON
JSON, JavaScript Object Notation, is basically a  specific syntax for organizing data as JavaScript objects
```javascript
{
    "kind": "grape",
    "color": "red",
    "quantity": 12,
    "tasty": true,
}
```

The only difference here is that our property names are now surrounded by double quotation marks "", making them string values

JSON objects, like all other JavaScript objects, can of course be stored in variables like
```javascript
const jsonFruit = {
    "kind": "grape",
    "color": "red",
    "quantity": 12,
    "tasty": true,
}
```

#### 5) GeoJSON
Just as JSON is just a formalization of existing JavaScript object syntax, GeoJSON objects are JSON objects, and all JSON objects are JavaScript objects.
GeoJSON can store points in geographical space (typically as longitude/latitude coordinates), but also shapes (such as lines and polygons) and other spatial features.
If you have a lot of geodata, it's worth it to parse it into GeoJSON format for best use with D3
```javascript
{
    "type": "FeatureCollection",
    "features": [
        {
        "type": "Feature",
        "geometry": {
                "type": "Point",
                "coordinates": [150.12824, -24.47125] 
                },
        "properties": {
            "type": "town"
            }
        }
    ]
}
```

### SVG
D3 is most useful when used to generate and manipulate visuals as Scalable Vector Graphics (SVG)
SVG is conceptually similar to HTML's canvas element.
At a minimum, it's good to specify `width` and `height` values. 
If you do not specify these, the SVG will behave like a typically greedy, block-level HTML element and take up as much room as it can within its enclosing element
```html
<svg width="500" height="50">
</svg>
```

*Extra*
The viewport is the visible area of the SVG image
If you do not specify any units inside `width` & `height` attributes, the units are assumed to be pixels
The list of the units you can use with the <svg> element
| Unit      | Description |
| ----------- | ----------- |
| em      | The default font size - usually the height of a charcter |
| ex   | The height of the character x                               |
| px   | Pixels                                                      |
| pt   | Points (1 / 72 of an inch)                                  |
| pc   | Picas (1 / 6 of an inch)                                    |
| cm   | Centimers                                                   |
| mm   | Millimeters                                                 |
| in   | Inches                                                      |

#### The View Box ex1)
```html
<svg width="500" height="200" viewBox="0 0 50 20" >

    <rect x="20" y="10" width="10" height="5"
          style="stroke: #000000; fill:none;"/>

</svg>
```
This example creates an <svg> element with a width of 500 pixels and a height of 200.
The viewBox attribute of the <svg> contains four coordinates. These coordinates define the view box of the <svg> element.
The coordinates are `x y width height` of the view box
in this case the view box starts at 0, 0 and is 50 wie and 20 high.
That means that the 500 by 200 pixels <svg> element internally uses a coordinate system that goes from 0, 0 to 50, 20.
In other words, every 1 unit in the coordinates used in the shapes inside the <svg> corresponds to 500/50 = 10 pixels in the width, and 200/20 = 10 pixels in the height.
That is why the rectangle with a x-position of 20 and an y-position of 10 is really located at 200, 100, and its width (10) and height (5) corresponds to 100 pixels and 50 pixels

#### The View Box ex2)
```html
 <svg width="500" height="200" viewBox="20 10 50 20" >
 
     <rect x="20" y="10" width="10" height="5"
           style="stroke: #000000; fill:none;"/>
 
 </svg>
 ```
원점. currently, the box is located at a coordinate (200,100) since the ratio is 1:10 for both width & height
changing the starting position x to 20 (20 * 10 == 200) and y to 10 (10 * 10 == 100), move the box to the original coordinate (0,0)

#### The View Box ex3)
```html
<svg width="200" height="200" viewBox="50 0 100 100"> 

<circle cx="50" cy="50" r="45" stroke="#000"
        stroke-width="3" fill="none"/> 
</svg>
```

#### Preserving Aspect Ratio
If the viewport and the view box does not have the same aspect ratio (width-to-height ratio), you need to specify how the SVG viwer (e.g. the browser) is to display the SVG image
Because the aspect ratio of an SVG image is defined by the `viewBox` attribute, if this attribute is not set, the `preserveAspectRatio` attribute has not effect
(with one exception, the `<image>` element)

All this reframing and scaling of vector graphics is great, but what if we (don't) want to maintain aspect ratio? How do we force an image to fill the entire width and height, even if that means stretching it one way or another?
By default, svg preserves this aspect ratio, which is often what you want - at any size, the graphic looks good because the proportions are all correct
But we can turn it off, or customize this behavior, using the `preserveAspectRatio` attribute

```javascript
preserveAspectRatio="align [meetOrSlice]"
```

align
 : none _ do not preserve aspect ratio
 : x<pos>y<pos> _ 3 values for <pos> min, mid and max
 
meetOrSlice (optional)
 : meet (default) _ scale up the graphic as much as possible, while preserving aspect ratio and making the entire viewbox visible within the viewport
 : covering the entire viewport with the viewbox
 
##### example PICTURE in this link 
(https://pandaqitutorials.com/Website/svg-aspect-ratio-grouping)

##### example CODE SNIPPET
https://codepen.io/jonitrythall/post/preserveaspectratio-in-svg

##### example YMin, YMid, and YMax
```html
<svg width="100" height="200" viewBox="0 0 50 50"
     preserveAspectRatio="xMinYMin meet"
     style="border: 1px solid #cccccc;">

    <circle cx="25" cy="25" r="25"
            style="stroke: #000000; fill:none;"/>

</svg>
```

### Simple Shapes
You can include a number of visual elements between those svg tags, including
rect , circle , ellipse , line , text , and path

#### Coordinates
0,0 is the top-left corner of the drawing space.
Increasing x values move to the right -->
Increasing y values move down

#### rect
needs following properties
x-position , y-position , width , height
```html
<rect x="0" y="0" width="500" height="50" />
```

#### circle
needs following properties
cx & cy : coordinates of the center
r : radius
```html
<circle cx="250" cy="25" r="25"
```
If svg has a width of 500, cx="250" gives the circle located in the middle.

#### ellipse
similar to circle, expects separate radius values for each axis
```html
<ellipse cx="250" cy="25" rx="100" ry="25" />
```

#### line
x1 & y1 to specify one end of the line
x2 & y2 to specify the coordinates of the other end
stroke : must be specified for the line to be visible

#### text
x : specify the position of the left edge
y : specify the verticle position of the type's baseline
 letters such as "p" and "y" extend below the baseline are called descenders
```html
<text x="250" y="25">Easy-peasy</text>
```
We could give CSS specified text / font style
```html
<text x="250" y="25" font-family="serif" font-size="25" fill="gray">
Easy-peasy
</text>
```

When any visual element runs up against the edge of the SVG, it will be clipped
Be careful when using `text` so your descenders do not get cut off
```html
<text x="250" y="50" font-family="serif" font-size="25" fill="gray">
Easy-peasy
</text>
```

### Styling SVG Element
SVG's default style is a black fill with no stroke. If you want anything else, you will have to apply styles to your elements
fill , stroke , stroke-width , opacity
```html
	<svg width="500" height="200" viewBox="0 0 50 20">
		<circle cx="10" cy="10" r="5" />
	</svg>
```

#### There are 2 ways to apply styles to an SVG Element

1_ directly (inline) as an attribute of the element
```html
<!-- Stroke width as a number -->    
		<circle cx="10" cy="10" r="5" fill="yellow" stroke="orange" stroke-width="5" />
```

2_ CSS style rule
```html
	<svg width="500" height="200" viewBox="0 0 50 20">

		<circle cx="10" cy="10" r="5" class="pumpkin" />
		
	</svg>
  
  <style>
    .pumpkin {
      fill: yellow;
      stroke: orange;
      stroke-width: 5;
    }
  </style>
```

#### CSS approach has a few obvious benefits
1_ You can specify a style once and have it applied to multiple elements
2_ CSS code is easier to read than inline attributes
3_ Maintaintable and faster to implement

*Important*
`fill, stroke, and stroke-width`, after all, are not CSS properties.
It's just that we are using CSS selectors to apply SVG-specific properties.
It's better to specify that it's SVG-specific by including `svg` in those selectors
```css
svg .pumpkin {

}
```

#### stroke-width
```html
	<svg width="500" height="200" viewBox="0 0 50 20">

<!-- Default stroke width: 1 -->    
		<circle cx="10" cy="10" r="5" fill="yellow" stroke="orange" />
    
<!-- Stroke width as a number -->    
		<circle cx="10" cy="10" r="5" fill="yellow" stroke="orange" stroke-width="5" />
    
<!-- Stroke width as a number -->    
    <circle cx="10" cy="10" r="5" fill="yellow" stroke="orange" stroke-width="10" />
    
 <!-- Stroke width as a percentage -->    
    <circle cx="10" cy="10" r="5" fill="yellow" stroke="orange" stroke-width="2%" />
		
	</svg>
```

#### layering and drawing order
Use Example Above

SVG does not support CSS's z-index property, so shapes can be arranged only within the two-dimensional x/y plane.
If we draw multiple shapes, they overlap.
The order in which elements are coded determines their depth order

### SVG browser compatibility
https://caniuse.com/?search=svg

