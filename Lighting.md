# Lighting Shaders

## Basic vertex for Lambert and Phong

```glsl
precision mediump float;

attribute vec3 position, normal;

uniform mat4 model, view, projection;
uniform mat4 inverseModel, inverseView, inverseProjection;
varying vec3 fragNormal, fragPosition;

void main() {
  vec4 viewPosition = view * model * vec4(position, 1.0);
  vec4 viewNormal = vec4(normal, 0.0) * inverseModel * inverseView;
  
  gl_Position = projection * viewPosition;
  fragNormal = viewNormal.xyz;
  fragPosition = viewPosition.xyz;
}
```

### Lambert fragment

```glsl
precision mediump float;

uniform vec3 ambient, diffuse, specular, lightDirection;
varying vec3 fragNormal, fragPosition;

void main() {
  vec3 eyeDirection = normalize(fragPosition);
  vec3 normal = normalize(fragNormal);
  vec3 light = normalize(lightDirection);
  
  float lambert = dot(normal, light);
  float phong = pow(max(dot(reflect(light, normal), eyeDirection), 0.0), shininess);

  vec3 lightColor = ambient + diffuse * lambert + specular * phong;
  gl_FragColor = vec4(lightColor, 1);
}
```

### Phong fragment

```glsl
precision mediump float;

uniform vec3 ambient, diffuse, specular, lightDirection;
uniform float shininess;
varying vec3 fragNormal, fragPosition;

void main() {
  vec3 eyeDirection = normalize(fragPosition);
  vec3 normal = normalize(fragNormal);
  vec3 light = normalize(lightDirection);
  
  float lambert = dot(normal, light);
  float phong = pow(max(dot(reflect(light, normal), eyeDirection), 0.0), shininess);

  vec3 lightColor = ambient + diffuse * lambert + specular * phong;
  gl_FragColor = vec4(lightColor, 1);
}
```
