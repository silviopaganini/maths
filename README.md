#Learning Maths again 

#### Radians / Degrees

```
// JavaScript
var angleInDegrees = 90;
var radians = angleInDegrees * Math.PI / 180;
var backToDegrees = radians * 180 / Math.PI;

// GLSL
float angleInDegrees = 90.0;
float r = radians(angleInDegrees);
float angleInDegrees = degrees(r);

```

####Calculate side lengths
##### SOHCAHTOA

```
// Javascript
var hyp = 100;
var angleDegrees = 45;

var opposite = Math.sin( (angleDegrees * Math.PI / 180) ) * hyp;
var adjacent = Math.cos( (angleDegrees * Math.PI / 180) ) * hyp;
var tangent  = opposite / adjacent;

// GLSL
float hyp = 100.;
float angleDegrees = 45.;

float opposite = sin(radians(angleDegrees)) * hyp;
float adjacent = cos(radians(angleDegrees)) * hyp;
float tangent  = opposite / adjacent;

```

####Linear Distance 2 points

```
// JavaScript
var x1 = 3;
var x2 = 5;
var distance = x2 — x1;

// GLSL
float x1 = 3.0;
float x2 = 5.0;
float distance = x2 — x1;
```

####Linear distance between 2 vectors

######Hypotenuse = a² + b² = c²

```
// Javascript
var v1 = {x: 4, y: -9};
var v2 = {x: 5, y: 15};

var distance = Math.sqrt( Math.pow((v2.x — v1.x), 2) + Math.pow((v2.y — v1.y), 2) );

// GLSL
vec2 x1 = vec2(1.0, 2.0);
vec2 x2 = vec2(2.0, 1.0);
float distance = distance(vec2(x1), vec2(x2));
```

####Length of a vector (Magnitude)

```
// Javascript
var v = {x: 4, y:-9};
var length = Math.sqrt( (Math.pow(v.x, 2) + Math.pow(v.y, 2)) );

var v = {x: 4, y:-9, z: 0.5};
var length = Math.sqrt( (Math.pow(v.x, 2) + Math.pow(v.y, 2)) + Math.pow(v.z, 2)) );

// GLSL
vec2 v = vec2(1.0, 2.0);
float l = length(v);
```

####Normalize vector

```
// Javascript
var v = {x: 4, y:-9};
var length = Math.sqrt( (Math.pow(v.x, 2) + Math.pow(v.y,2)) );
var n = {x: v.x / length, y: v.y / length};

// GLSL
vec2 v = vec2(4.0, -9.0);
vec2 n = normalize(v);
```

####Dot product vectors

```
// Javascript
var v1 = {x: 4, y: 5, z: 9};
var v2 = {x: 5, y: 9, z: -5};
var dot = (v1.x * v2.x) + (v1.y * v2.y) + (v1.z * v2.z);

// GLSL 
vec3 v1 = vec2(4., 5., 9.);
vec3 v2 = vec2(5., 9., -5.);
float dot = dot(v1, v2);
```

#### Finding angle(degrees and radians) between vectors

```
// Javascript
var v1 = {x: 4, y: 5, z: 9};
var v2 = {x: 5, y: 9, z: -5};
var dot = (v1.x * v2.x) + (v1.y * v2.y) + (v1.z * v2.z);

var lengthv1 = length(v1); // see length
var lengthv2 = length(v2); // see length

var radians = Math.acos(dot / (lengthv1 * lengthv2));
var angle = radians * 180 / Math.PI;


// GLSL 
vec3 v1 = vec2(4., 5., 9.);
vec3 v2 = vec2(5., 9., -5.);
float dot = dot(v1, v2);
float l1 = length(v1);
float l2 = length(v2);

float radians = acos(dot / (l1 * l2));
float angle = degrees(radians);
```

