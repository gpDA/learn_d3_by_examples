### <Head/> What does it do
- Loading data into the browser's memory
- Binding data to elements within the document, creating new elements as needed
- Transforming those elements by interpreting each element's bound datum and setting its visual properties accordingly
- Transitioning elements between states in response to user input

### <Head/> Alternatives
#### ++ Easy Charts ++
Data Wrapper
Flot
Google Chart Tools
Highcharts
Peity
Timeline.js

#### <Head/> ++ Graph Visualizations ++
Arbor.js
Cytoscape.js
Sigma.js

#### ++ Geomapping ++
Kartograph
Leaflet
Modest Maps
Polymaps

#### ++ programming from scratch ++
p5.js
Paper.js
Raphael
Snap.svg
Two.js

#### ++ Three-Dimensional ++
==> D3 is not the best at a 3D, simply because web browsers are historically two-dimensional beasts. 
But with increased support for WebGL, there are now more opportunities for 3D web experiences 
PhiloGL
Three.js

#### ++ Tools Built with D3 ++
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

### <Head/> CSS Rules
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

### <Head/> JavaScript variable
1) Arrays
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

2) Objects
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

3) Objects and Arrays
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

4) JSON
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

5) GeoJSON
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
