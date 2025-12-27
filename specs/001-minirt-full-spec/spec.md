# Feature Specification: Full miniRT Implementation with Bonuses

**Feature Branch**: `001-minirt-full-spec`  
**Created**: 2025-12-27  
**Status**: Draft  
**Input**: User description: "현재 디렉토리에 miniRT.pdf 파일 참고해서 요구사항 명세 정리. bonus 과제 모두 구현."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Render a Simple Scene with Basic Objects (Priority: P1)

As a user, I want to execute the ray tracer program with a valid `.rt` scene file as an argument. The program should parse the scene, render it, and display the final image in a window. The scene will contain basic geometric objects (spheres, planes, cylinders) with ambient and diffuse lighting, and hard shadows.

**Why this priority**: This is the core functionality of the project, demonstrating the ability to parse a scene and produce a rendered image.

**Independent Test**: Can be tested by running the program with a simple scene file (e.g., `scenes/simple.rt`). The test passes if the rendered image correctly displays the objects with proper lighting and shadows as defined in the scene file.

**Acceptance Scenarios**:

1. **Given** a `.rt` file defining a scene with a camera, an ambient light, a spot light, a sphere, a plane, and a cylinder.
   **When** the user runs the program with the scene file as an argument.
   **Then** a window appears displaying the correctly rendered image from the camera's perspective, with objects colored, lit, and casting shadows.

---


### User Story 2 - Control the Render Window (Priority: P2)

As a user, I want to be able to close the render window and terminate the program cleanly.

**Why this priority**: Provides essential user control over the application.

**Independent Test**: Can be tested by running the program and attempting to close the window.

**Acceptance Scenarios**:

1. **Given** the render window is open.
   **When** the user presses the `ESC` key.
   **Then** the window closes and the program exits without errors or resource leaks.
2. **Given** the render window is open.
   **When** the user clicks the window's native close button.
   **Then** the window closes and the program exits without errors or resource leaks.

---


### User Story 3 - Handle Invalid Scene Files (Priority: P3)

As a scene author, when I provide an invalid or malformed `.rt` scene file, I want the program to exit gracefully and print a clear, descriptive error message.

**Why this priority**: Crucial for usability, allowing users to debug their scene files.

**Independent Test**: Can be tested by running the program with an invalid scene file (e.g., `scenes/invalid.rt`). Passes if the program exits with a non-zero status and prints a helpful error message.

**Acceptance Scenarios**:

1. **Given** a `.rt` file with a syntax error (e.g., missing value, incorrect identifier).
   **When** the user runs the program with the invalid scene file.
   **Then** the program prints a standard error message (e.g., "Error\n") followed by a descriptive message and exits.
2. **Given** a `.rt` file where a unique element (like Camera) is defined more than once.
   **When** the user runs the program with that scene file.
   **Then** the program prints an error message indicating that the element must be unique and exits.

---


### User Story 4 - Render Advanced and Bonus Features (Priority: P4)

As a user, I want to render scenes that include bonus features, such as specular reflection, checkerboard patterns, bump mapping, additional object types (cone), and multiple colored spot lights.

**Why this priority**: This covers all the bonus objectives, demonstrating a more advanced and feature-rich ray tracer.

**Independent Test**: Can be tested by running the program with a scene file containing bonus features. Passes if the rendered image shows all features correctly.

**Acceptance Scenarios**:

1. **Given** a scene with an object and a light source.
   **When** the scene is rendered.
   **Then** the object shows specular highlights (shiny spots) in addition to diffuse and ambient light.
2. **Given** a scene with a plane defined with a checkerboard pattern.
   **When** the scene is rendered.
   **Then** the plane is textured with a black and white checkerboard pattern.
3. **Given** a scene with a cone object.
   **When** the scene is rendered.
   **Then** the cone is displayed correctly with proper lighting and intersections.

### Edge Cases

- **Empty Scene File**: The program should handle an empty `.rt` file gracefully, printing an error message.
- **No Lights**: A scene with no light sources should render objects with only the ambient light color.
- **Object Intersections**: The program must correctly render complex scenarios where objects intersect or are positioned inside one another.
- **Out-of-view Objects**: Objects defined in the scene but positioned outside the camera's field of view should not be visible.

## Requirements *(mandatory)*

### Functional Requirements

#### Mandatory Requirements
- **FR-001**: The system MUST be a command-line executable.
- **FR-002**: The system MUST accept one argument: the path to a scene description file with a `.rt` extension.
- **FR-003**: The system MUST parse the `.rt` file to construct an in-memory representation of the 3D scene.
- **FR-004**: The parser MUST support: Ambient lightning (A), Camera (C), Light (L), Sphere (sp), Plane (pl), and Cylinder (cy).
- **FR-005**: The parser MUST be flexible regarding whitespace and newlines between element properties.
- **FR-006**: The system MUST validate the scene file and exit with a descriptive error message if the file is malformed, contains invalid values, or defines unique elements (A, C) more than once.
- **FR-007**: The system MUST implement a ray tracing rendering engine.
- **FR-008**: The renderer MUST calculate intersections for rays with spheres, planes, and cylinders.
- **FR-009**: The lighting model MUST include Ambient and Diffuse components.
- **FR-010**: The renderer MUST calculate hard shadows cast by objects.
- **FR-011**: The system MUST support translation and rotation transformations for all applicable objects and the camera.
- **FR-012**: The system MUST display the rendered image in a graphical window.
- **FR-013**: The application MUST terminate cleanly when the 'ESC' key is pressed or the window's close button is clicked.
- **FR-014**: The system MUST NOT support geometric shapes or lighting effects beyond those explicitly specified in this document (Mandatory and Bonus sections).
- **FR-015**: The system MAY provide minimal additional logging to standard error for scene parsing issues (e.g., warnings for ignored lines or minor deviations from strict parsing rules that don't cause an immediate error).
- **FR-016**: The system MUST NOT support runtime scene modification or dynamic interaction with rendered objects (beyond closing the window and resizing objects).

#### Bonus Requirements
- **FR-100**: The lighting model MAY be extended to a full Phong reflection model, including a Specular component.
- **FR-101**: The system MAY support multiple, colored spot lights.
- **FR-102**: The system MAY support applying a checkerboard pattern to any object's surface.
- **FR-103**: The system MAY implement one additional 2nd-degree object type (e.g., Cone, Hyperboloid, Paraboloid).
- **FR-104**: The system MAY support texture mapping on objects.

### Dependencies and Assumptions

#### Dependencies
- **DEP-001**: The system requires a graphical environment capable of displaying a window and capturing keyboard/mouse events.
- **DEP-002**: A graphics library for window management, drawing pixels, and handling events is required.

#### Assumptions
- **ASM-001**: The mathematical formulas for ray-object intersections and the Phong lighting model are assumed to be based on standard computer graphics literature.
- **ASM-002**: The format of the `.rt` scene file is fixed as per the definitions in the source document.
- **ASM-003**: "Cleanly" exiting the program implies no resource leaks (memory, file handles, etc.).
- **ASM-004**: The maximum number of objects (spheres, planes, cylinders, etc.) expected in a single scene file is around 50.

### Key Entities 

- **Scene**: Represents the entire 3D world to be rendered. Contains a camera, lights, and a list of objects.
- **Camera**: Defines the viewpoint, orientation, and field of view (FOV) from which the scene is rendered.
- **Light**: An entity that illuminates the scene. Can be ambient or a spot light.
- **Object**: A geometric shape in the scene (Sphere, Plane, Cylinder, Cone).
- **Material**: Properties describing an object's surface, such as color and texture.
- **Ray**: A vector with an origin and a direction.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: The final rendered image must be pixel-perfect according to the specified ray tracing algorithms for all shapes and lighting.
- **SC-002**: The application must not have any memory or resource leaks, verified by standard profiling tools.
- **SC-003**: The application must compile without any warnings or errors under a strict set of compiler flags.
- **SC-004**: All valid scenes provided in the project subject must render correctly.
- **SC-005**: For any invalid scene, the program must return a non-zero exit code and print a helpful, human-readable error message.
- **SC-006**: Window and event handling must be responsive and function as specified 100% of the time.
- **SC-007**: The application should target a rendering frame rate of 30 FPS for a typical scene (around 50 objects) to ensure responsiveness.
- **SC-008** (Bonus): Visuals for bonus features must be mathematically correct and match reference implementations.

## Clarifications

### Session 2025-12-27

- Q: What are the expected maximum number of objects (spheres, planes, cylinders) in a scene? → A: around 50
- Q: What is the target rendering time or frame rate for a typical scene (e.g., a scene with "around 50" objects)? → A: 30 FPS for responsiveness
- Q: Are there any additional geometric shapes or lighting effects beyond those specified in the mandatory and bonus sections that are explicitly out of scope for this project? → A: Only the specified shapes and lighting models are in scope.
- Q: Beyond error messages, is any runtime logging or output expected (e.g., scene parsing details, performance metrics, scene object count)? → A: Minimal additional logging for scene parsing issues.
- Q: Is there any expectation for runtime scene modification or dynamic interaction with rendered objects (beyond closing the window and resizing objects)? → A: No runtime scene modification or dynamic interaction is expected.
