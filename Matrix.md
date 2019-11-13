#Matrix transformations

Using homogeneous coordinates

###Translation

```
[
  1, 0, 0, 0,
  0, 1, 0, 0,
  0, 0, 1, 0,
  t.x, t.y, t.z, 1
]
```

###Scale

```
[
  s.x, 0, 0, 0,
  0, s.y, 0, 0,
  0, 0, s.z, 0,
  0, 0, 0, 1
]
```

<!-- ###Rotation

```
[
  rot.x, 0, 0, 0,
  0, rot.y, 0, 0,
  0, 0, rot.z, 0,
  0, 0, 0, 1
]
``` -->

```glsl
mat4 rotationMatrix(vec3 axis, float angle) {
    axis = normalize(axis);
    float s = sin(angle);
    float c = cos(angle);
    float oc = 1.0 - c;

    return mat4(oc * axis.x * axis.x + c,           oc * axis.x * axis.y - axis.z * s,  oc * axis.z * axis.x + axis.y * s,  0.0,
                oc * axis.x * axis.y + axis.z * s,  oc * axis.y * axis.y + c,           oc * axis.y * axis.z - axis.x * s,  0.0,
                oc * axis.z * axis.x - axis.y * s,  oc * axis.y * axis.z + axis.x * s,  oc * axis.z * axis.z + c,           0.0,
                0.0,                                0.0,                                0.0,                                1.0);
}

vec3 rotate(vec3 v, vec3 axis, float angle) {
    mat4 m = rotationMatrix(axis, angle);
    return (m * vec4(v, 1.0)).xyz;
}
```
