# Data Model: miniRT

This document outlines the key data entities for the miniRT ray tracer, based on the feature specification.

## Entities

### `Vector`
Represents a 3D vector or point in space.
- **Fields**:
  - `x`: double
  - `y`: double
  - `z`: double

### `Color`
Represents an RGB color.
- **Fields**:
  - `r`: integer (0-255)
  - `g`: integer (0-255)
  - `b`: integer (0-255)

### `Ray`
Represents a ray used for tracing.
- **Fields**:
  - `origin`: Vector
  - `direction`: Vector (normalized)

### `Material`
Describes the surface properties of an object.
- **Fields**:
  - `color`: Color
  - `specular_intensity`: double (Bonus)
  - `texture`: Texture (Bonus)

### `Object` (Interface/Base Type)
A generic interface for a geometric shape in the scene. All objects must be intersectable by a ray.
- **Subtypes**: `Sphere`, `Plane`, `Cylinder`, `Cone`

### `Sphere`
- **Fields**:
  - `center`: Vector
  - `diameter`: double
  - `material`: Material

### `Plane`
- **Fields**:
  - `point`: Vector
  - `normal`: Vector (normalized)
  - `material`: Material

### `Cylinder`
- **Fields**:
  - `center`: Vector
  - `axis`: Vector (normalized)
  - `diameter`: double
  - `height`: double
  - `material`: Material

### `Cone` (Bonus)
- **Fields**:
  - `center`: Vector
  - `axis`: Vector (normalized)
  - `angle`: double
  - `material`: Material

### `Light` (Interface/Base Type)
An entity that illuminates the scene.
- **Subtypes**: `AmbientLight`, `SpotLight`

### `AmbientLight`
Provides constant illumination to the entire scene.
- **Fields**:
  - `ratio`: double (0.0-1.0)
  - `color`: Color

### `SpotLight`
A point light source.
- **Fields**:
  - `position`: Vector
  - `ratio`: double (0.0-1.0)
  - `color`: Color (Bonus)

### `Camera`
Defines the viewpoint for rendering.
- **Fields**:
  - `viewpoint`: Vector
  - `orientation`: Vector (normalized)
  - `fov`: integer (0-180 degrees)

### `Scene`
The top-level container for the entire 3D world.
- **Fields**:
  - `camera`: Camera
  - `ambient_light`: AmbientLight
  - `lights`: List<SpotLight>
  - `objects`: List<Object>

## Relationships

- A `Scene` contains one `Camera`, one `AmbientLight`, a list of `SpotLight`s, and a list of `Object`s.
- Each `Object` has one `Material`.
- `Light` and `Object` are polymorphic types.

## State Transitions

The data model is static after the initial parsing of the `.rt` file. There are no state transitions during runtime as per the clarified specification (no dynamic interaction).
