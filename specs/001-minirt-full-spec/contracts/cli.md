# Contract: Command-Line Interface and Scene File Format

This document defines the primary external contracts for the `miniRT` application.

## 1. Command-Line Interface (CLI)

The application is invoked via a single command-line entry point.

### Invocation

```sh
./miniRT <scene_file>
```

### Arguments

- **`<scene_file>`** (Required)
  - **Type**: `string`
  - **Description**: The relative or absolute path to a valid scene description file.
  - **Constraints**: The file must have a `.rt` extension.

### Exit Codes

- **`0`**: Success. The program executed, rendered the scene (if valid), and exited cleanly.
- **`1`** (or other non-zero value): Error. Used for all error conditions, such as file parsing errors, invalid arguments, or runtime issues. An error message must be printed to standard error.

## 2. Scene File Format (`.rt`)

The `.rt` file is a plain text file that describes the objects, lights, and camera in a 3D scene.

- **Encoding**: UTF-8
- **Syntax**:
  - Each element is defined on its own line.
  - The first piece of information on a line is the element's **type identifier**.
  - Information for an element is separated by one or more whitespace characters.
  - The order of elements in the file does not matter.
  - Lines that are empty or do not start with a valid type identifier should be ignored (or trigger a warning, as per FR-015).

### Element Definitions

#### **`A` - Ambient Lightning** (Unique)
- **Format**: `A <ratio> <r,g,b>`
- **`ratio`**: `double` in range `[0.0, 1.0]`. The ambient lighting ratio.
- **`r,g,b`**: `integer` in range `[0, 255]`. The color of the ambient light.

#### **`C` - Camera** (Unique)
- **Format**: `C <x,y,z> <nx,ny,nz> <fov>`
- **`x,y,z`**: `double`. The coordinates of the viewpoint.
- **`nx,ny,nz`**: `double` in range `[-1, 1]`. The normalized orientation vector.
- **`fov`**: `integer` in range `[0, 180]`. The horizontal field of view in degrees.

#### **`L` - Light**
- **Format**: `L <x,y,z> <ratio> <r,g,b>`
- **`x,y,z`**: `double`. The coordinates of the light point.
- **`ratio`**: `double` in range `[0.0, 1.0]`. The light brightness ratio.
- **`r,g,b`**: `integer` in range `[0, 255]`. The color of the light (Bonus).

#### **`sp` - Sphere**
- **Format**: `sp <x,y,z> <diameter> <r,g,b>`
- **`x,y,z`**: `double`. The coordinates of the sphere's center.
- **`diameter`**: `double`. The diameter of the sphere.
- **`r,g,b`**: `integer` in range `[0, 255]`. The color of the sphere.

#### **`pl` - Plane**
- **Format**: `pl <x,y,z> <nx,ny,nz> <r,g,b>`
- **`x,y,z`**: `double`. Coordinates of a point on the plane.
- **`nx,ny,nz`**: `double` in range `[-1, 1]`. The normalized normal vector.
- **`r,g,b`**: `integer` in range `[0, 255]`. The color of the plane.

#### **`cy` - Cylinder**
- **Format**: `cy <x,y,z> <nx,ny,nz> <diameter> <height> <r,g,b>`
- **`x,y,z`**: `double`. The coordinates of the center of the cylinder.
- **`nx,ny,nz`**: `double` in range `[-1, 1]`. The normalized axis vector.
- **`diameter`**: `double`. The diameter of the cylinder.
- **`height`**: `double`. The height of the cylinder.
- **`r,g,b`**: `integer` in range `[0, 255]`. The color of the cylinder.

---

*This contract is derived from the feature specification and the original `miniRT.pdf` document.*
