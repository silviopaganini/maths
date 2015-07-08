#Useful GLSL Functions

### world normal
```glsl
varying vec3 vNormal;
varying vec3 vPosition;

vec4 worldNormal = vec4(normal, 0.0) * inverseModel * inverseView;

vNormal = worldNormal.xyz;

```

### bisector angle
```glsl
vec3 bisector(vec3 a, vec3 b) {
  return normalize(length(b) * a + length(a) * b);
}
```

### reflect point
```glsl
vec3 reflectPoint(vec3 p, vec3 n) {
  return p - 2.0 * dot(n, p) * n / dot(n, n);
}
```

### rotate 2D point (Matrix)
```glsl
vec2 rotate2D(vec2 position, float theta)
{
    // theta in radians
    mat2 m = mat2( cos(theta), sin(theta), -sin(theta), cos(theta) );
    return m * position;
}
```

### rotate 3D point (matrix)
```glsl

vec3 rotatePoint(vec3 p, vec3 n, float theta) {

// p is the point to be rotated
// n is the rotation vector normalized
// theta is the amount in radians

  return (
    p * cos(theta) + cross(n, p) *
    sin(theta) + n * dot(p, n) *
    (1.0 - cos(theta))
  );
}

 mat4 rotation = mat4(
 	rotatePoint(vec3(1, 0, 0), n, theta), 0,
 	rotatePoint(vec3(0, 1, 0), n, theta), 0, 
 	rotatePoint(vec3(0, 0, 1), n, theta), 0,
 	0, 0, 0, 1
 );
 
vec4 rotatedPosition = rotation * vec4(position, 1.0);
```

### return bool if point is inside box
```glsl
bool inTile(vec2 p, float tileSize) {
  vec2 ptile = step(0.5, fract(0.5 * p / tileSize));
  return ptile.x == ptile.y;
}
```

### return bool if point within circle boundaries
```glsl
bool inCircle(vec2 point, vec2 center, float radius) {
    point -= center;
    return length(point) <= radius;
}
```
###power matrices

```glsl
mat2 matrixPower(highp mat2 m, int n) {

  highp mat2 p = mat2(1.0) * m;
  for(int i = 1; i< 16 ; i++) {
    if(i == n) return p;
    p *= m;
  }
  return p;
}
```