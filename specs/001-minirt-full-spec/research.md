# Research: Graphics Library for miniRT

## Decision

We will use **SDL2 (Simple DirectMedia Layer)** as the primary graphics and windowing library for this project.

## Rationale

The feature specification requires a graphics library for window management, pixel plotting, and event handling on both Linux and macOS. Our research identified several candidates, with SDL2 being the most suitable choice.

- **Cross-Platform**: SDL2 is a mature, stable, and widely-used library with excellent support for Linux, macOS, and Windows, which aligns with the project's constitution (Principle V).
- **Low-Level Access**: It provides the necessary low-level access to the frame buffer (pixel buffer), which is ideal for a software renderer like a ray tracer where we need to plot pixels manually.
- **Rich Feature Set**: It includes robust support for window creation, 2D rendering, and a simple event loop for handling keyboard (`ESC` key) and window close events.
- **Community & Documentation**: As a popular library, SDL2 has extensive documentation, tutorials, and a large community, which will be invaluable for development and troubleshooting.
- **Performance**: SDL can leverage hardware acceleration for 2D rendering, but for our purposes, its software rendering backend is sufficient and performant for plotting pixel buffers.

This choice directly addresses the dependency `DEP-002` in the feature specification.

## Alternatives Considered

- **NOT_MLX**: This is a portable wrapper around SDL2 designed specifically to be an alternative to `miniLibX`. While it offers a familiar API, using SDL2 directly provides more flexibility, direct access to a larger feature set, and avoids adding another layer of abstraction.
- **Raylib**: A very good, simple-to-use library. However, SDL is more established and has a larger community, making it a lower-risk choice for this project.
- **Allegro**: Similar to SDL, but SDL is generally considered more common and has a larger user base.
- **Cairo**: More focused on vector graphics, making it less ideal for the direct, raster-based pixel manipulation required for this ray tracer.
