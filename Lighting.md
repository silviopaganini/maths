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
  vec4 viewNormal = vec4(normal, 0.0) * inverseModel * inverseView;
  
  gl_Position = projection * viewPosition;
  vNormal = viewNormal.xyz;
  vPosition = viewPosition.xyz;
}
```

### Lambert

```glsl
float lambert(vec3 n, vec3 d)
{
	// n : surface view normal
	// d : direction of the light
	return dot(n, normalize(d));
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
