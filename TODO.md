# Laocoön — Bronze and Time

## Deliver a single-file cinematic landing page
- [x] The website is a pure HTML/CSS/JS implementation with a self-contained `index.html`, no framework, no bundler, and no build step; Three.js r0.160 and its matching `GLTFLoader` are loaded through a CDN import map.
- [x] The document has `lang="en"`, title `The Statue of Laocoön`, UTF-8 metadata, responsive viewport metadata, a `900vh` body, fixed canvas/overlay UI, hidden scrollbars, and a hidden native cursor.

## Deliver the WebGL bronze sculpture stage
- [x] The full-screen WebGL canvas renders against pure black with `FogExp2('#000000', 0.01)`, the specified perspective camera, ACES filmic tone mapping, exposure `2.2`, pixel ratio capped at `2`, soft shadows, and the requested ambient, key, rim, and fill lighting.
- [x] The supplied `bronze_horse.glb` asset is loaded from the specified asset base URL, wrapped in a pivot, assigned semi-polished bronze material values (`roughness 0.42`, `metalness 0.92`), smooth shading, shadow flags, auto-scaled to max dimension `3.5`, recentered, and lowered to pivot `y = -0.4`.
- [x] Scroll position drives a smoothed full `360°` camera orbit with the requested `phi`, `y`, radius, look-at offset, camera lerp, and first-screen text clearance.

## Deliver shader, particles, and motion
- [x] The camera-local background plane uses the specified slow liquid-bronze wave shader, constant wave frequencies/angles/weights, scroll deformation, mouse shift, bronze-to-sapphire palette interpolation, crest multiplier, vignette, and depth settings.
- [x] The scene creates exactly `450` additive point sparks with procedural radial-gradient texture, 60% molten orange / 40% icy blue colors, specified particle size/opacity, per-particle motion data, scroll-velocity turbulence, and recycle bounds.
- [x] Pointer handling snaps the inner cursor, lerps the outer ring, updates normalized mouse targets, tilts the model with the specified lerps, and resizes the renderer and shader resolution.

## Deliver editorial navigation and chapters
- [x] The fixed header contains the Laocoön brand, Bronze/Marble/Fluid/Digital navigation, dot separators, and Contact pill; navigation uses target scroll values `[0.0, 0.34, 0.62, 0.94]` with smooth scrolling.
- [x] Four editorial slides use the exact supplied copy and active ranges `[-0.10, 0.12]`, `[0.28, 0.40]`, `[0.56, 0.68]`, and `[0.84, 1.05]` with per-letter blur-up title reveals and delayed description reveals.
- [x] The supplied `1.png` asset is revealed in the slide-two mask with the requested clip-path wipe and scale transition.
- [x] The five vertical grid lines, horizontal divider, drifting dots, and four story progress dashes update from the smoothed scroll position.

## Serve and preview the website
- [x] A minimal Node static server listens on `0.0.0.0:3000` and serves the page and the required `/manus-routes.json` route manifest.
- [x] Project metadata includes a durable HTTPS `logoUrl` for the Laocoön asset.
