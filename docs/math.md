# math

Neverfair extends the standard Lua `math` table with vector and angle helpers. Standard functions like `math.sin`, `math.cos`, and `math.sqrt` are still available.

## calc_angle

```lua
math.calc_angle(src: vec3_t, dst: vec3_t): angle_t
```

Returns the angle from `src` to `dst`.

## calc_fov

```lua
math.calc_fov(src: angle_t, dst: angle_t): number
```

Returns field-of-view delta between two angles.

## normalize_angle

```lua
math.normalize_angle(angle: angle_t): angle_t
```

Normalizes pitch and yaw.

## vector_angles

```lua
math.vector_angles(vec: vec3_t): angle_t
```

Converts a direction vector to angles.

## angle_vectors

```lua
math.angle_vectors(angle: angle_t): vec3_t, vec3_t, vec3_t
```

Returns `forward`, `right`, and `up` vectors.

```lua
local forward = math.angle_vectors(g_camera_angles)
```

See [`vec3_t`](types.md#vec3_t) and [`angle_t`](types.md#angle_t).
