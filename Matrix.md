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

###Rotation

```
[ 
  rot.x, 0, 0, 0, 
  0, rot.y, 0, 0,
  0, 0, rot.z, 0,
  0, 0, 0, 1
]
```