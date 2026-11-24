# GARGANTUA

A real-time black hole raytracer in a single HTML page. Follow light through Schwarzschild spacetime to see a star field bend around a non-rotating black hole, the far side of an accretion disk appear above its shadow, and the approaching side of the disk glow brighter than the receding side.

## Quick start

1. Download `gargantua.html` and open it in a browser with **WebGL 2** and hardware acceleration enabled. No installation, build step, or network connection is required.
2. Press **3** for the *Edge* view to see how light bends around the shadow. Switch to **4** for the *Polar* view to compare the same disk nearly face-on.
3. Press **H** to hide the display, or **C** to start a continuous sequence through all four views. Sound is off until you enable it.

## Controls

| Action | Mouse or touch | Keyboard |
| --- | --- | --- |
| Orbit | Drag the scene | Arrow keys |
| Zoom | Scroll, or adjust **Observer distance** in **Params** | `+` / `−` |
| Choose a camera | Select **Cinematic**, **Poster**, **Edge**, or **Polar** | `1`, `2`, `3`, `4`, respectively |
| Toggle the automatic camera sequence | Select **Sequence** | `C` |
| Open or close parameters | Select **Params** or its close button | `P`; `Esc` closes the panel |
| Toggle ambient sound | Select **Sound** | `S` |
| Hide or restore the display | Select **HUD −** or **Show HUD** | `H` |

**Cinematic** is a fixed camera preset; **Sequence** moves between presets. Orbiting, zooming, or changing the inclination gives you manual control again.

## Parameters and telemetry

| Parameter | Range or options | What changes |
| --- | --- | --- |
| Observer distance | 13–55 gravitational radii | Moves the observer toward or away from the black hole rather than cropping the image. |
| Disk inclination | 0°–89° | Sets the viewing angle measured from the disk normal: 0° is face-on; 89° is nearly edge-on. |
| Geodesic step budget | 48–240 steps | Controls integration accuracy. Rays that reach the horizon or escape stop early. |
| Render profile | Performance · Balanced · Fine | Changes image resolution independently of the integration step budget. |

The HUD shows mission elapsed time, observer distance, disk inclination, step budget, active render profile, and measured frame rate. **For a smoother orbit, try Performance first**: it reduces the number of rays without lowering the accuracy of each ray.

## How the image is made

- **Light bending.** A WebGL 2 fragment shader follows each ray in its orbital plane. A fourth-order Runge–Kutta integrator advances the Schwarzschild null-geodesic equation in inverse radius. Escaping rays sample a procedural star field; captured rays contribute no background light.
- **Accretion disk.** When a ray crosses the disk plane between 6 and 12 gravitational radii, it samples a textured emission band. A ray can cross the plane more than once, revealing additional images of the disk. Orbital Doppler beaming and gravitational frequency shifts modulate the emission.
- **Photon-ring highlight.** The renderer adds a narrow highlight at the Schwarzschild critical curve to suggest higher-order images too thin to resolve at the selected resolution. The highlight is an approximation, not a fully resolved sequence of photon rings.

This is an interactive visualization, not a precision scientific renderer. The model assumes a non-rotating black hole and a thin emitting disk; it does not simulate Kerr frame dragging or plasma dynamics.

## Publish with GitHub Pages

To serve GARGANTUA at the root of a project site, copy `gargantua.html` to `index.html` in the repository root and commit it. Under **Settings → Pages**, choose **Deploy from a branch**, select the branch containing `index.html` and the **/ (root)** folder, then save. No build command is needed. If you keep the original filename instead, open `gargantua.html` under the published site URL.

