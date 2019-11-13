# Learning Maths again 

### [Useful GLSL Functions](https://github.com/silviopaganini/maths/blob/master/GLSL.md)

### [Basic light shading](https://github.com/silviopaganini/maths/blob/master/Lighting.md)

thanks to everyone who created the [Shader School](https://www.npmjs.com/package/shader-school) =) 

## Contents

- [Radians / Degrees](#radians--degrees)
- [Calculate side lengths](#calculate-side-lengths)
- [Rotate a 2D point](#rotate-a-2d-point)
- [Linear Distance 2 points](#linear-distance-2-points)
- [Linear distance between 2 vectors](#linear-distance-between-2-vectors)
- [Length of a vector](#length-of-a-vector)
- [Add and substract vectors](#add-and-substract-vectors)
- [Normalize vector](#normalize-vector)
- [Dot product vectors](#dot-product-vectors)
- [Finding angle between 2 points](#finding-angle-between-2-points)
- [Finding angle between 2 vectors](#finding-angle-between-2-vectors)
- [Cross Product](#cross-product)

#### Radians & Degrees

```js
// JavaScript
var angleInDegrees = 45;
var radians = angleInDegrees * Math.PI / 180;
var backToDegrees = radians * 180 / Math.PI;
```

```glsl
// GLSL
float angleInDegrees = 90.0;
float r = radians(angleInDegrees);
float angleInDegrees = degrees(r);
```

#### Calculate side lengths
##### SOHCAHTOA

```js
// Javascript
var hyp = 100;
var angleDegrees = 45;
var angleRadians = angleDegrees * Math.PI / 180;

var opposite = Math.sin( angleRadians ) * hyp;
var adjacent = Math.cos( angleRadians ) * hyp;
var tangent  = opposite / adjacent;
```

```glsl
// GLSL
float hyp = 100.;
float angleDegrees = 45.;
float angleRadians = radians(angleDegrees);

float opposite = sin(angleRadians) * hyp;
float adjacent = cos(angleRadians) * hyp;
float tangent  = opposite / adjacent;

```

#### Rotate a 2D point
```js
var vec2 = {x: 2, y: 3};
var rotatedVector = rotate2D(vec2, angle);

function rotate2D(vector, angle)
{
	var theta = angle * Math.PI / 180; // radians
	var matrix = [  Math.cos(theta),  Math.sin(theta), 
					-Math.sin(theta), Math.cos(theta)
					];
					
	return { 
		x: matrix[0] * vector.x + matrix[1] * vector.y, 
		y: matrix[2] * vector.x + matrix[3] * vector.y
	};
}

```

```glsl
// GLSL
vec2 rotate2D(vec2 position, float theta)
{
    // theta in radians
    mat2 m = mat2( cos(theta), sin(theta), -sin(theta), cos(theta) );
    return m * position;
}
```

#### Linear Distance 2 points

```js
// JavaScript
var x1 = 3;
var x2 = 5;
var distance = x2 — x1;
```

```glsl
// GLSL
float x1 = 3.0;
float x2 = 5.0;
float distance = x2 — x1;
```

#### Linear distance between 2 vectors

###### a² + b² = c²

```js
// Javascript
var v1 = {x: 4, y: -9};
var v2 = {x: 5, y: 15};

var distance = Math.sqrt( Math.pow((v2.x — v1.x), 2) + Math.pow((v2.y — v1.y), 2) );
```

```glsl
// GLSL
vec2 x1 = vec2(1.0, 2.0);
vec2 x2 = vec2(2.0, 1.0);
float distance = distance(vec2(x1), vec2(x2));
```

#### Length of a vector
###### a.k.a Magnitude 

```js
// Javascript
// 2D -> hypotenuse
var v = {x: 4, y:-9};
var length = Math.sqrt( (Math.pow(v.x, 2) + Math.pow(v.y, 2)) );

// 3D
var v = {x: 4, y:-9, z: 0.5};
var length = Math.sqrt( (Math.pow(v.x, 2) + Math.pow(v.y, 2) + Math.pow(v.z, 2) ));
```

```glsl
// GLSL
vec2 v = vec2(1.0, 2.0);
float l = length(v);
```

#### Add and substract vectors

```js
var v1 = {x: 2, y: 3};
var v2 = {x: 2, y: -2};
var addedVec = {x: v1.x + v2.x, y: v1.y + v2.y};
var subVec = {x: v1.x - v2.x, y: v1.y - v2.y};
```

#### Normalize vector

```js
// Javascript
// 2D
var v = {x: 4, y:-9};
var length = Math.sqrt( (Math.pow(v.x, 2) + Math.pow(v.y,2)) );
var n = {x: v.x / length, y: v.y / length};

// 3D
var v = {x: 4, y:-9, z: 3};
var length = Math.sqrt( Math.pow(v.x, 2) + Math.pow(v.y,2) + Math.pow(v.z,2) );
var n = {x: v.x / length, y: v.y / length, z: v.z / length};
```

```glsl
// GLSL
vec2 v = vec2(4.0, -9.0);
vec2 n = normalize(v);

vec3 v = vec3(4.0, -9.0, 3.0);
vec3 n = normalize(v);
```

#### Dot product vectors

```js
// Javascript
var v1 = {x: 4, y: 5, z: 9};
var v2 = {x: 5, y: 9, z: -5};
var dot = (v1.x * v2.x) + (v1.y * v2.y) + (v1.z * v2.z);
```
```glsl
// GLSL 
vec3 v1 = vec2(4., 5., 9.);
vec3 v2 = vec2(5., 9., -5.);
float dot = dot(v1, v2);
```

#### Finding angle between 2 points

```js
//Javascript
var x = -3;
var y = -2;
var radians = Math.atan2(x, y);
var degrees = radians * 180 / Math.PI;
```

```glsl
//GLSL
float x = -3.0;
float y = -2.0;
float radians = atan(x, y);
float degrees = degrees(radians);
```

#### Finding angle between 2 vectors

```js
// Javascript
var v1 = {x: 4, y: 5, z: 9};
var v2 = {x: 5, y: 9, z: -5};
var dot = (v1.x * v2.x) + (v1.y * v2.y) + (v1.z * v2.z);

var lengthv1 = length(v1); // see length
var lengthv2 = length(v2); // see length

var radians = Math.acos(dot / (lengthv1 * lengthv2));
var angle = radians * 180 / Math.PI;
```
```glsl
// GLSL 
vec3 v1 = vec2(4., 5., 9.);
vec3 v2 = vec2(5., 9., -5.);
float dot = dot(v1, v2);
float l1 = length(v1);
float l2 = length(v2);

float radians = acos(dot / (l1 * l2));
float angle = degrees(radians);
```

#### Cross Product

```js
// Javascript
var v1 = {x: 1, y: 2, z: 3};
var v2 = {x: 3, y: 2, z: 1};
var cross = {
	x: v1.y*v2.z - v1.z*v2.y, 
	y: v1.z*v2.x - v1.x*v2.z, 
	z: v1.x*v2.y - v1.y*v2.x
};

```
```glsl
// GLSL
vec3 v1 = vec3(1.0, 2.0, 3.0);
vec3 v2 = vec3(2.0, 2.0, 1.0);
vec3 cross = cross(v1, v2);
```

#### Projection of point B over A


![](data:image/gif;base64,R0lGODdhegBFAIAAAAAAAP///ywAAAAAegBFAAAC/oyPqcvtD6OctEqAgd28+5ll30iWYBia6mqiLgvHmyvK9v3QGM73B+0L4l4aoXFVTB2XpaJB5GRKK9HnlLmzVBPb6y1L6XqxSogYcR6zsuBGWm1kv98/OE/uoNuDeIa+vmfTp/AX2IPip2WItdjIxVHoSBIpuUT5WPmV2XhJuBnT+XnXJKoSWipoijpyugrTmug6IzsGS0sKenuhO2Wbw5sHzDgk7Fkc5+MbqHwcJsT81eZmWuaKOE0NhJapzaXzDR5+za2DJn6Onq6+zo4uCF76PdQd/3JXvTp+D1zTfOgP0FA/VJGksdJg0F/CSdAgBeiHMAnEMBFbDLTkRCIgUisPKeKDVLHXto4bSRbccXFGSClRkozkePKHr4/IALUcGfNJwys3SXKESVHnzl4Zf/o06U2MPWERi5oDo3QByqE8HSYNiE0RTqyxghJayDWshwIAOw==)

```js
// Javascript
// ||b -> a|| 
var b = {x: 1, y: 3};
var theta = 45;
var projection = normalize(b) * Math.cos(theta); // see Normalize Vector
```

```glsl
// GLSL
vec2 b = vec2(1, 3);
float theta = 45;
float projection = normalize(b) * cos(theta);
```