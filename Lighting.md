# Lighting

## Basic vertex for Lambert and Phong

```glsl
precision mediump float;

attribute vec3 position, normal;

uniform mat4 model, view, projection;
uniform mat4 inverseModel, inverseView, inverseProjection;
varying vec3 vNormal, vPosition;

void main() {
  vec4 viewPosition = view * model * vec4(position, 1.0);
  
  // important : normal with inverse transforms
  vec4 viewNormal = vec4(normal, 0.) * inverseModel * inverseView;
  
  gl_Position = projection * viewPosition;
  vNormal = viewNormal.xyz;
  vPosition = viewPosition.xyz;
}
```

### Lambert

```glsl
float lambert(vec3 n, vec3 d)
{
	// n : surface view normalized
	// d : direction of the light normalized
	return dot(n, d);
}
```

### Phong

```glsl
float phong(vec3 light, vec3 normal, vec3 eyeDirection, float shininess)
{
	// light        : normalized light direction
	// normal       : surface view normal
	// eyeDirection : normalized vPosition
	// shininess    : self explanatory =) 

    return pow(max(dot(reflect(light, normal), eyeDirection), 0.0), shininess);
}
```

### Creating color

```glsl
vec3 eyeDirection = normalize(vPosition);
vec3 light = ambient + 
        diffuse * lambert(vNormal, lightDirection) + 
        specular * phong( 
        	normalize(lightDirection), 
        	vNormal, 
        	eyeDirection, 
        	shininess 
        );
```

### Gooch shading

```glsl

float goochWeight(vec3 normal, vec3 lightDirection) {
  return 0.5 * (1.0 + dot(normal, lightDirection));
}

vec3 goochColor(vec3 cool, vec3 warm, float weight) {
  return mix(cool, warm, weight);
}

float weight = goochWeight(normal, light);
vec3 normal = normalize(vNormal);
vec3 light = normalize(lightDirection);
vec3 lightColor = goochColor(cool, warm, wight);
gl_FragColor = vec4(lightColor,1);

```
