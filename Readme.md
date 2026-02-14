Blob Mixer
===========

Interactive Three.js demo that morphs a glossy blob across multiple styles and titles. Use the mouse wheel to switch between presets; the scene animates the mesh, gradient, background, and text transitions.

![Blob Mixer Preview](https://res.cloudinary.com/dcjobwnp5/image/upload/v1771085174/image_14_op1qgh.png)

Features
--------
- Custom vertex-displacement blob shader driven by 4D simplex noise
- Preset switching with smooth GSAP transitions
- Gradient texture swapping for different looks
- Animated 3D text titles using a custom vertex shader
- HDRI environment lighting for realistic reflections

Tech Stack
----------
- Three.js for the 3D scene, camera, renderer, materials, and geometry
- three-custom-shader-material to inject custom vertex code into MeshPhysicalMaterial
- troika-three-text for high-quality signed-distance-field text
- GSAP for timeline-style transitions
- Vite + vite-plugin-glsl to bundle JS and GLSL
- Tailwind CSS (currently minimal usage, just imported)

Project Structure (what is used where)
-------------------------------------
- index.html
	- Canvas entry point (`#canvas`) and app mount.

- src/main.js
	- Scene setup: renderer, camera, tone mapping, resize handling.
	- Blob presets: `blobs[]` defines name, background color, and shader/material config.
	- CustomShaderMaterial: extends MeshPhysicalMaterial with `vertexShaders.glsl`.
	- Geometry: high-detail icosahedron merged/tangent-computed for smooth shading.
	- HDR environment: RGBE loader pulls a studio HDRI for reflections.
	- Text: `troika-three-text` with `textVertexShader.glsl` for animated title swap.
	- Animation loop: updates time uniform and renders.
	- Scroll interaction: GSAP transitions between presets and updates uniforms.

- src/style.css
	- Tailwind import (no extra CSS currently).

- src/Shaders/vertexShaders.glsl
	- Blob displacement logic.
	- Uses 4D simplex noise to perturb positions and recompute normals for lighting.

- src/Shaders/simplexNoise4d.glsl
	- 4D simplex noise implementation used by the blob vertex shader.

- src/Shaders/fragmentShaders.glsl
	- Placeholder fragment shader (not wired in main.js yet).

- src/Shaders/textVertexShader.glsl
	- Twirl/rotate animation for the text during preset transitions.

- public/gradients/
	- PNG gradients used as the blob's `map` texture per preset.

- public/configvals.js
	- Alternate preset definitions (not used by `main.js` yet).

Getting Started
--------------
1) Install dependencies
	 npm install

2) Run dev server
	 npm run dev

![Blob Mixer Preview](https://res.cloudinary.com/dcjobwnp5/image/upload/v1771085172/image_12_ipl3jm.png)


Controls
--------
- Mouse wheel: switch between blob presets

I Learn From This Project
------------------------------------
- A Three.js scene with HDRI lighting and physical materials
- Inject custom GLSL into standard materials using three-custom-shader-material
- Animate shader uniforms and material properties with GSAP
- Drive mesh deformation using 4D simplex noise
- Render crisp animated text in 3D with troika-three-text
- Bundle GLSL and assets in Vite

![Blob Mixer Preview](https://res.cloudinary.com/dcjobwnp5/image/upload/v1771085174/image_13_dnznzm.png)


