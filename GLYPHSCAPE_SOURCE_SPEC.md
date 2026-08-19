# APPLICATION BUILD PROMPT: GLYPHSCAPE

## GLYPHSCAPE — 3D ASCII World Simulator

Build a complete browser-based creative simulation application called **GLYPHSCAPE**.

**GLYPHSCAPE** is a local-first procedural world generator, editor, simulator, and capture studio that renders true three-dimensional environments as animated ASCII art.

The application should let a user move from:

**SEED → SHAPE → POPULATE → SIMULATE → OBSERVE → CAPTURE**

Users should be able to generate a world, sculpt or edit it, introduce vegetation and inhabitants, run environmental simulations, explore the world using a 3D camera, customize how it is translated into characters, and export still or animated ASCII artwork.

The guiding idea is:

> A living world, rendered one character at a time.

GLYPHSCAPE must not be merely:

- A static text-art generator
- A 2D tile-map editor
- A filter applied to prerecorded video
- A collection of canned animations
- A terminal window with decorative controls

It must maintain an actual three-dimensional world model, a movable camera, lighting, entities, simulation state, and a real-time ASCII rendering pipeline.

---

## 1. PRODUCT CHARACTER

GLYPHSCAPE should feel like a combination of:

- A procedural terrain generator
- A miniature world simulator
- A voxel or diorama editor
- A cinematic camera tool
- A shader and ASCII-art laboratory
- A living model railroad viewed through a terminal

The ASCII viewport is the heart of the application. Controls should support the viewport rather than overwhelm it.

The interface should feel precise, atmospheric, creative, and highly polished. It can draw visual inspiration from old terminals and scientific instruments, but it should not become a parody of retro computing.

Use:

- Strong monospace typography
- Clean panel geometry
- Restrained terminal-inspired accents
- Excellent contrast
- Subtle depth and animation
- Clear active states
- Large, readable controls
- Collapsible work areas
- A dominant central viewport

Avoid:

- Excessive neon effects
- Fake CRT distortion by default
- Tiny illegible labels
- Overcrowded toolbars
- Low-contrast gray-on-black text
- Decorative controls that do nothing
- Constantly moving backgrounds
- Modal dialogs for routine operations

---

## 2. CORE EXPERIENCE

A new user should be able to:

1. Choose a world preset.
2. Enter or randomize a seed.
3. Select a visual mood.
4. Generate a world.
5. Orbit or fly through it.
6. Start the simulation.
7. Watch weather, vegetation, water, lighting, and inhabitants evolve.
8. Adjust the ASCII style.
9. Capture the current frame or record an animation.

An experienced user should be able to:

1. Construct a procedural generation recipe.
2. Control terrain, hydrology, climate, biomes, structures, and population.
3. Sculpt and paint the world manually.
4. Inspect individual cells, objects, and agents.
5. Trigger environmental events.
6. Adjust simulation speed and subsystem behavior.
7. Define custom glyph ramps and semantic symbols.
8. Create camera bookmarks and animated camera paths.
9. Save checkpoints and branch alternate versions of a world.
10. Export reproducible projects and high-quality artwork.

---

## 3. NON-NEGOTIABLE REQUIREMENTS

GLYPHSCAPE must be:

- Local-first
- Private by default
- Fully functional without an account
- Free of telemetry
- Free of advertising
- Usable without a backend
- Capable of running offline after installation or first load
- Deterministic when the same seed and settings are used
- Responsive on common desktop and laptop displays
- Usable as a read-only viewer on tablets and phones

Every visible control must work.

Do not create placeholder buttons, dead menu items, nonfunctional export options, or panels labeled “coming soon.”

Display a visible semantic version number such as:

**GLYPHSCAPE v1.0.0**

The application must include:

- Autosave
- Autosave status indicator
- Undo and redo
- JSON project import and export
- Explicit New World command
- Explicit Load Demo command
- Clear Local Data command
- Keyboard shortcuts
- Contextual help
- Error handling
- Project schema versioning
- Safe migration of older saved projects

Do not silently load a demo world as the user’s project. Demo content must be intentionally selected.

---

## 4. WORLD MODEL

Use a true three-dimensional scene.

A hybrid world representation is appropriate:

- Height-field terrain for large landforms
- Sparse voxel or block data for caves, cliffs, structures, and edited regions
- Instanced geometry for vegetation and repeated objects
- Particle systems for rain, snow, ash, sparks, mist, and dust
- Agent entities for animals, inhabitants, vehicles, or abstract life
- A water surface and simplified water-state model
- Separate simulation grids for temperature, moisture, wind, fertility, and population

Keep simulation resolution independent from visual output resolution.

For example, the world might contain a 128 × 128 simulation grid while being rendered to an 80 × 45, 120 × 68, or 200 × 112 character display.

The project should track:

- World seed
- World dimensions
- Terrain data
- Material data
- Water level
- Climate maps
- Biome assignments
- Objects and structures
- Agents
- Simulation clock
- Current season
- Weather state
- Event history
- Camera state
- Camera bookmarks
- Render settings
- Glyph settings
- Named checkpoints
- Project metadata

---

## 5. PROCEDURAL WORLD GENERATOR

Provide a procedural generation system with reproducible seeds.

### World seed controls

Include:

- Text or numeric seed
- Randomize Seed
- Copy Seed
- Lock Seed
- Regenerate
- Mutate World
- Mutate Only Unlocked Parameters
- Previous Seed
- Next Seed

The same seed and settings must reproduce the same initial world.

### World forms

Provide several initial world forms:

- Island
- Archipelago
- River valley
- Mountain range
- Forest basin
- Desert canyon
- Storm coast
- Volcanic landscape
- Polar landscape
- Ruined city
- Floating islands
- Asteroid or miniature planetoid
- Empty sculpting world

### Terrain controls

Support controls such as:

- World width and depth
- Maximum elevation
- Sea level
- Base terrain scale
- Noise frequency
- Noise octaves
- Persistence
- Lacunarity
- Ridge strength
- Valley depth
- Plateau strength
- Coastal falloff
- Island mask
- Crater density
- Cave density
- Cliff threshold
- Erosion intensity
- Sediment smoothing
- River count
- Lake frequency
- Terrain roughness
- Terrain exaggeration

Allow users to lock individual parameters before randomizing or mutating the rest of the world.

### Procedural recipe stack

Advanced Mode should expose the generation process as an ordered recipe stack.

Possible recipe operations include:

- Base elevation
- Continental mask
- Fractal noise
- Ridged noise
- Voronoi regions
- Terrace
- Crater
- Canyon
- Hydraulic erosion
- Thermal erosion
- Coastline shaping
- River carving
- Cave carving
- Material assignment
- Biome assignment
- Structure placement
- Vegetation placement
- Population placement

Users should be able to:

- Add operations
- Remove operations
- Reorder operations
- Enable or disable operations
- Duplicate operations
- Edit operation parameters
- Save a recipe as a preset
- Export and import recipes

---

## 6. CLIMATE AND BIOME GENERATION

Generate derived world maps for:

- Elevation
- Slope
- Temperature
- Moisture
- Rainfall
- Wind
- Drainage
- Fertility
- Sun exposure
- Distance from water
- Biome
- Habitability

Biome assignment should respond to elevation, temperature, moisture, and proximity to water.

Initial biome types can include:

- Ocean
- Beach
- Grassland
- Shrubland
- Temperate forest
- Rainforest
- Taiga
- Tundra
- Desert
- Marsh
- Alpine
- Volcanic
- Urban
- Ruin
- Ice

Provide debug overlays for each derived map.

These overlays should be inspectable in the viewport but automatically hidden from normal artwork exports unless explicitly enabled.

---

## 7. SIMULATION SYSTEMS

The world must be able to evolve after generation.

Use a fixed-timestep simulation so behavior remains deterministic and does not change dramatically based on frame rate.

Each simulation subsystem must be individually enabled or disabled.

### Time and light

Support:

- Time of day
- Day and night cycle
- Sun angle
- Moon or secondary light
- Adjustable day length
- Seasons
- Latitude
- Seasonal temperature shift
- Sunrise and sunset
- Simulation calendar
- Freeze Lighting command

### Weather

Support stylized weather states such as:

- Clear
- Cloudy
- Fog
- Rain
- Heavy rain
- Thunderstorm
- Snow
- Blizzard
- Dust storm
- Ashfall
- High wind

Weather should affect appropriate world properties such as:

- Visibility
- Light level
- Moisture
- Vegetation
- Fire behavior
- Agent movement
- Water accumulation

Weather can be generated automatically or triggered manually.

### Hydrology

Use a simplified, performance-conscious hydrology model.

Support:

- Rain accumulation
- Drainage direction
- Streams
- Rivers
- Lakes
- Flooded cells
- Evaporation
- Drought
- Water-source placement

Do not attempt a computationally expensive fluid simulation across every visual voxel.

### Vegetation

Vegetation should be able to:

- Spawn in suitable biomes
- Grow over time
- Spread to neighboring cells
- Respond to moisture and fertility
- Die during drought
- Burn during fire
- Regrow after disturbance

Vegetation types can include:

- Grass
- Shrubs
- Deciduous trees
- Conifer trees
- Reeds
- Cacti
- Fungi
- Alien flora

### Fire

Provide a stylized fire-spread simulation influenced by:

- Available fuel
- Moisture
- Wind direction
- Wind strength
- Slope
- Rain
- Firebreaks

Users should be able to place an ignition point and observe the spread.

### Agents and inhabitants

Provide lightweight agents that make the world feel alive.

Possible agent categories include:

- Wildlife
- Settlers
- Explorers
- Vehicles
- Boats
- Flying creatures
- Abstract particles or spirits

Simple behaviors can include:

- Wander
- Seek water
- Seek food
- Avoid danger
- Follow roads
- Follow terrain contours
- Gather resources
- Return home
- Build a simple shelter
- Flee fire
- Rest at night

Do not attempt to create a massive artificial-intelligence simulation. A small number of readable, inspectable agents is preferable to thousands of meaningless entities.

### Events

Allow the user to trigger events such as:

- Storm
- Flood
- Drought
- Wildfire
- Earthquake
- Volcanic eruption
- Meteor impact
- Vegetation bloom
- Migration
- Settlement arrival
- Abandonment
- Blackout
- Sunrise
- Eclipse

Record events in a simulation log.

Clearly describe the simulation as a creative, stylized model rather than a scientific forecasting tool.

---

## 8. SIMULATION CONTROLS

Provide prominent controls for:

- Play
- Pause
- Stop
- Reset to Initial State
- Advance One Tick
- Advance One Hour
- Advance One Day
- Simulation Speed
- Slow Motion
- Real-Time Mode
- Maximum-Speed Mode

Suggested simulation speed values:

- 0.25×
- 0.5×
- 1×
- 2×
- 5×
- 10×
- 50×
- 100×

Display:

- Current simulation date and time
- Current tick
- Current season
- Current weather
- Active event count
- Agent count
- Frames per second
- Simulation updates per second

Allow the world to be paused while the camera and render settings remain interactive.

---

## 9. ASCII RENDERING ENGINE

Implement a custom real-time ASCII rendering pipeline.

Three.js or an equivalent local 3D library may be used for scene management, cameras, lighting, and geometry. Do not rely solely on an unmodified stock ASCII-effect plugin.

A suitable rendering process is:

1. Render the 3D scene to a low-resolution offscreen buffer.
2. Collect brightness, color, depth, material, surface-normal, and edge information where practical.
3. Divide the result into character cells.
4. Map each cell to one or more glyphs.
5. Apply color and styling.
6. Draw the result efficiently into a canvas.
7. Maintain a parallel text representation for copying and text export.

Do not create one HTML element per character. That approach will perform poorly at useful resolutions.

### Render modes

Include:

**Shaded ASCII**

Characters are selected primarily from luminance and surface lighting.

**Semantic ASCII**

Characters represent world materials or objects, such as water, trees, roads, buildings, and agents.

**Hybrid ASCII**

Semantic characters are modified according to lighting, depth, and surface direction.

**Outline ASCII**

Edges and silhouettes dominate the rendering.

**Depth ASCII**

Characters represent distance from the camera.

**Wireframe ASCII**

Geometry edges and structural lines are emphasized.

**Braille Detail**

Use Unicode Braille characters for a higher-density point representation.

**Block Detail**

Use Unicode block characters for dense, graphic output.

### Glyph ramps

Include editable glyph ramps.

Example ramps may include:

- Minimal
- Classic
- Soft
- Dense
- Blocks
- Technical
- Organic
- Stipple
- Braille
- User-defined

Provide a glyph-ramp editor where the user can:

- Enter characters
- Reorder characters
- Reverse the ramp
- Remove ambiguous characters
- Preview density
- Save the ramp
- Import or export a ramp

Correct for the non-square aspect ratio of monospace character cells.

### Semantic glyph map

Allow users to assign characters to materials and entities.

Examples:

- Water
- Grass
- Dirt
- Sand
- Rock
- Snow
- Tree
- Shrub
- Road
- Building
- Ruin
- Fire
- Rain
- Animal
- Person
- Vehicle

Semantic assignments should allow several glyph variants so repeated objects do not look unnaturally identical.

### Color modes

Support:

- Monochrome
- Two-tone
- ANSI 16-color
- ANSI 256-color
- Full RGB
- Material colors
- Depth gradient
- Heat-map colors
- Custom palette

Include accessible palettes and color-blind-friendly presets.

### Rendering controls

Provide controls for:

- Character width
- Character height
- Output columns
- Output rows
- Automatic resolution
- Adaptive resolution
- Character spacing
- Line spacing
- Font size
- Font weight
- Background color
- Foreground color
- Contrast
- Gamma
- Brightness
- Exposure
- Edge strength
- Outline threshold
- Dithering
- Noise
- Fog
- Depth fade
- Shadow strength
- Highlight strength
- Surface-normal influence
- Semantic influence
- Color saturation
- Transparency
- Frame blending
- Motion trails
- Scanlines
- CRT curvature
- Flicker

Retro effects such as scanlines, curvature, bloom, ghosting, and flicker must be optional and disabled by default.

---

## 10. CAMERA AND NAVIGATION

Support several camera modes:

- Orbit
- Free Fly
- First Person
- Ground Walk
- Top Down
- Isometric
- Orthographic
- Cinematic Path
- Auto Tour

### Mouse controls

Use a clearly visible distinction between **Navigate** and **Edit** tools so the user does not accidentally modify the world while trying to move the camera.

Suggested navigation behavior:

- Left drag: orbit or look
- Middle drag: pan
- Right drag: alternate orbit or context action
- Mouse wheel: zoom or change movement speed
- Double-click: focus location
- Shift: accelerate movement
- Alt or Option: precision movement

Allow remapping in Settings.

### Keyboard controls

Include:

- `W A S D` — Move
- `Q / E` — Move down and up
- Arrow keys — Look or orbit
- `Shift` — Move faster
- `Space` — Play or pause simulation
- `.` — Advance one simulation tick
- `F` — Focus selection
- `G` — Toggle grid
- `H` — Hide interface
- `R` — Regenerate when appropriate
- `1–9` — Recall camera bookmarks
- `Ctrl/Cmd + Z` — Undo
- `Ctrl/Cmd + Shift + Z` — Redo
- `Ctrl/Cmd + S` — Save project
- `Esc` — Exit current tool or close overlay

### Camera bookmarks

Allow users to:

- Save named camera positions
- Reorder bookmarks
- Assign number shortcuts
- Store projection and render settings with a bookmark
- Create a thumbnail
- Restore a bookmark
- Use bookmarks as camera-path keyframes

### Camera paths

Provide a simple keyframe editor for:

- Position
- Look target
- Field of view
- Projection
- Duration
- Easing
- Pause time
- Render-setting changes

Allow playback and recording of a camera path.

---

## 11. WORLD EDITING TOOLS

Provide an explicit editing mode with undoable actions.

### Terrain tools

Include:

- Raise
- Lower
- Smooth
- Flatten
- Terrace
- Noise
- Erode
- Dig
- Fill
- Carve river
- Add crater
- Create cliff
- Set sea level

Brush controls should include:

- Radius
- Strength
- Falloff
- Shape
- Surface-only mode
- Continuous mode

### Material painting

Allow users to paint:

- Soil
- Rock
- Sand
- Snow
- Grass
- Water
- Road
- Structure foundation
- Burned terrain
- User-defined materials

### Object placement

Provide a local object palette containing procedural low-poly or voxel-style objects such as:

- Tree
- Shrub
- Rock
- Grass patch
- House
- Tower
- Ruin
- Bridge
- Road segment
- Dock
- Boat
- Campfire
- Lamp
- Water source
- Agent spawn
- Weather emitter
- Event trigger
- Camera marker

Support:

- Place
- Move
- Rotate
- Scale
- Duplicate
- Delete
- Multi-select
- Box select
- Group
- Lock
- Hide

### Protected regions

Allow users to lock selected areas so procedural regeneration does not overwrite them.

This makes it possible to manually construct a village and then regenerate the surrounding landscape.

---

## 12. INSPECTION AND OBSERVABILITY

Clicking a world location should open an inspector showing available information such as:

- Coordinates
- Elevation
- Slope
- Material
- Biome
- Temperature
- Moisture
- Fertility
- Water depth
- Wind
- Light level
- Vegetation
- Fire state
- Occupying object
- Occupying agent
- Recent events

Clicking an agent should show:

- Name or identifier
- Type
- Current behavior
- Destination
- Energy
- Health
- Inventory
- Home location
- Recent actions

Provide visual overlays for:

- Height
- Slope
- Temperature
- Moisture
- Rainfall
- Water flow
- Wind
- Fertility
- Biomes
- Vegetation density
- Fire risk
- Agent paths
- Population density
- Lighting
- Render depth
- Render edges

Include a compact world statistics panel showing values such as:

- Land area
- Water area
- Average elevation
- Highest point
- Biome proportions
- Vegetation coverage
- Structure count
- Agent count
- Active fire cells
- Current rainfall
- Estimated simulation load

---

## 13. USER INTERFACE

### Top bar

Include:

- GLYPHSCAPE name
- Visible version
- Project name
- New
- Open
- Save
- Import
- Export
- Undo
- Redo
- Easy/Advanced Mode
- Help
- Settings
- Fullscreen

### Left panel: World Lab

Use collapsible sections or tabs for:

- Generate
- Terrain
- Climate
- Biomes
- Populate
- Events
- Simulation
- ASCII Style
- Camera
- Capture

### Center viewport

The central viewport should:

- Occupy most of the screen
- Remain usable when panels collapse
- Support fullscreen
- Display ASCII without clipping
- Preserve correct character proportions
- Show an optional center reticle
- Show selection outlines without corrupting the exported artwork
- Support interface-free presentation mode

### Right panel: Inspector

Show context-sensitive controls for:

- Selected cell
- Selected object
- Selected agent
- Selected procedural operation
- Current camera
- Current render style
- Current event

### Bottom area

Include a collapsible bottom drawer containing:

- Simulation timeline
- Event log
- Camera path
- Performance monitor
- World statistics
- Generation messages
- Validation warnings

### Status bar

Show:

- Autosave status
- Seed
- Simulation state
- Date and time
- ASCII resolution
- Frames per second
- Active tool
- Current camera mode
- Offline status

Autosave states should be visually distinct:

- Unsaved
- Saving
- Saved
- Save error

---

## 14. EASY MODE

Easy Mode should make the application understandable without exposing every procedural parameter.

Show only:

- World Type
- Seed
- Randomize
- Mood
- World Complexity
- Population Level
- Weather
- Time of Day
- ASCII Style
- Color Style
- Generate
- Play/Pause
- Camera Mode
- Snapshot
- Record
- Export

Provide attractive preset cards with thumbnails.

A user should be able to create an interesting animated world in less than a minute.

Easy Mode must not be a separate or fake implementation. It should manipulate the same underlying project model as Advanced Mode.

---

## 15. ADVANCED MODE

Advanced Mode should expose:

- Full generation recipe
- Terrain parameters
- Hydrology settings
- Climate settings
- Biome rules
- Simulation subsystem controls
- Agent behavior parameters
- Event controls
- Full glyph editor
- Semantic glyph assignments
- Render passes
- Camera keyframes
- Debug overlays
- Performance settings
- Project metadata
- Data import and export tools

Switching between Easy and Advanced Mode must not lose data.

---

## 16. BUILT-IN WORLD PRESETS

Include polished presets such as:

### Misty Archipelago

Small islands, shallow water, fog, sparse trees, quiet waves, and slow daylight.

### Alpine Night

Sharp mountains, snow, moonlight, deep shadows, and occasional snowfall.

### Living Forest

Dense vegetation, rain, wildlife, streams, growth, and seasonal change.

### Storm Coast

Cliffs, high winds, heavy rain, rough water, and distant lightning.

### Emberlands

Volcanic terrain, ash, lava glow, fire, smoke, and sparse resilient vegetation.

### Desert Caravan

Dunes, rock formations, a moving group of agents, heat haze, and a long sunset.

### Ruined City

Collapsed buildings, roads, vegetation reclamation, fog, and wandering inhabitants.

### Floating Garden

Floating landmasses, waterfalls, airborne particles, unusual vegetation, and flying agents.

### Tiny Planet

A miniature spherical or strongly curved world with a dramatic horizon.

### Blank Diorama

An empty world intended for manual sculpting and object placement.

Each preset must remain fully editable.

---

## 17. CHECKPOINTS, HISTORY, AND BRANCHING

Allow users to create named checkpoints containing:

- World state
- Simulation time
- Camera state
- Render settings
- Thumbnail
- Notes

Users should be able to:

- Restore a checkpoint
- Duplicate a checkpoint as a new branch
- Compare basic statistics
- Rename it
- Delete it
- Export it
- Continue simulating from it

For deterministic replay, preserve:

- Original seed
- Initial parameters
- User edits
- Triggered events
- Simulation timing
- Random-number-generator state where practical

Full continuous rewind is not required. Periodic snapshots plus an event log are acceptable.

---

## 18. IMPORT AND EXPORT

### Project formats

Support:

- Full project JSON
- Procedural recipe JSON
- Glyph-ramp JSON
- Palette JSON
- Camera-path JSON
- Checkpoint export
- Simulation event log

### World import

Where practical, support:

- Grayscale PNG heightmaps
- CSV heightmaps
- JSON voxel or terrain data
- Custom palette files
- Plain-text semantic maps

### Artwork export

Support:

- Copy Current Frame to Clipboard
- Plain-text `.txt`
- ANSI `.ans`
- ANSI-colored text
- HTML with styled monospace text
- SVG made from text rows
- PNG
- Transparent PNG
- High-resolution PNG
- Animated GIF
- WebM recording
- Standalone looping HTML viewer

Animation export should provide:

- Width and height
- Character resolution
- Frame rate
- Duration
- Loop toggle
- Camera source
- Interface inclusion
- Transparent or solid background
- Metadata inclusion
- Simulation-speed control

Exports must preserve character-cell alignment.

Do not add a watermark. Optional project metadata may be included only when the user enables it.

---

## 19. LOCAL STORAGE AND PROJECT SAFETY

Use:

- IndexedDB for projects, checkpoints, and larger state
- Local storage only for compact preferences
- A versioned project schema
- Defensive parsing for imported files
- Clear validation errors
- Safe defaults when optional fields are missing

Autosave should occur after meaningful changes without blocking the interface.

Provide separate commands for:

- New World
- Reset Current Simulation
- Clear Current Project
- Delete Saved Project
- Clear All Local Data

Destructive actions must be clearly distinguished and confirmed.

Do not intentionally clear local project data following an application error.

If initialization fails, show a readable recovery screen containing:

- Error summary
- Application version
- Option to retry
- Option to export recoverable project data
- Option to start without loading the last project
- Technical details that can be copied

---

## 20. PERFORMANCE

Target smooth interaction on a typical modern laptop.

Use:

- Typed arrays
- Instanced geometry
- Chunked world updates
- Level of detail
- Web Workers for generation and simulation where useful
- Fixed simulation timestep
- Adaptive ASCII resolution
- Frame-budget monitoring
- Cached glyph metrics
- Efficient canvas text rendering
- Paused updates for hidden panels
- Throttled inspector updates
- Spatial indexing for objects and agents

Provide quality settings:

- Draft
- Standard
- High
- Custom

Draft quality should favor responsiveness during editing. High quality should favor artwork capture.

The application should degrade gracefully when a world exceeds the current device’s performance capability. Display a clear warning and suggest reducing:

- World size
- Agent count
- Simulation rate
- Particle count
- Shadow quality
- ASCII resolution

Do not allow a runaway simulation loop to freeze the entire interface.

---

## 21. ACCESSIBILITY

Include:

- High-contrast interface
- Adjustable UI scale
- Adjustable ASCII font size
- Reduced-motion mode
- Disable Flicker option
- Color-blind-friendly palettes
- Keyboard navigation
- Visible focus states
- Tooltips
- Text labels in addition to icons
- Screen-reader labels for major controls
- Confirmation before destructive actions

ASCII output should remain interpretable in monochrome mode.

Do not use color as the only indicator of state.

---

## 22. PRIVACY AND OFFLINE OPERATION

GLYPHSCAPE must not transmit:

- Project data
- Seeds
- Generated worlds
- Captures
- Usage information
- Device information
- Imported files

No telemetry, analytics, tracking pixels, advertising scripts, or behavioral profiling.

If third-party libraries are used, bundle them locally or provide a fully offline build.

Include a concise Privacy and Local Storage section explaining:

- What is stored
- Where it is stored
- That project data remains on the device
- How the user can export it
- How the user can delete it

---

## 23. HELP AND ONBOARDING

Provide a short first-run introduction explaining:

1. Choose a preset or blank world.
2. Generate the world.
3. Navigate with the mouse or keyboard.
4. Press Play to run the simulation.
5. Open ASCII Style to change the appearance.
6. Capture or export the result.

Include:

- Shortcut reference
- Mouse-control reference
- Explanation of seeds
- Explanation of Easy and Advanced Mode
- Explanation of simulation limitations
- Explanation of checkpoints
- Explanation of export formats

Do not force the user through a long onboarding sequence.

---

## 24. TECHNICAL IMPLEMENTATION

Prefer a client-side static application.

A practical architecture may use:

- HTML
- CSS
- Modern JavaScript
- Three.js or equivalent for 3D scene management
- Custom ASCII post-processing
- Canvas for the visible character renderer
- Web Workers for expensive generation
- IndexedDB for projects
- Service worker for offline availability

Prefer a self-contained `index.html` when practical. If maintainability or library size makes that unreasonable, use a small static file structure with no server-side dependency and no required build service.

The application should run from ordinary static hosting.

Avoid a mandatory Node.js, Python, database, or cloud backend.

Organize the code into clear systems such as:

- ProjectStore
- WorldGenerator
- TerrainModel
- ClimateModel
- SimulationClock
- WeatherSystem
- HydrologySystem
- VegetationSystem
- FireSystem
- AgentSystem
- EventSystem
- SceneRenderer
- AsciiRenderer
- CameraController
- SelectionManager
- HistoryManager
- ExportManager
- UIController

Document important algorithms and non-obvious performance decisions.

---

## 25. ACCEPTANCE CRITERIA

The completed application must demonstrate all of the following:

1. A world can be generated from a seed.
2. Using the same seed and settings reproduces the same starting world.
3. The world is a true navigable 3D scene.
4. The scene is rendered as animated ASCII art.
5. The user can orbit, fly, zoom, and focus the camera.
6. The user can play, pause, reset, and single-step the simulation.
7. Lighting changes over time.
8. At least weather, vegetation, and agents can evolve.
9. At least one environmental event can be triggered.
10. Terrain can be manually edited.
11. Objects can be placed, selected, moved, and deleted.
12. Undo and redo work.
13. ASCII glyph ramps can be changed.
14. Semantic, shaded, and hybrid render modes work.
15. Monochrome and color modes work.
16. A frame can be copied as plain text.
17. PNG and text exports work.
18. At least one animated export format works.
19. Projects survive a browser refresh.
20. JSON export and import reproduce the project.
21. Easy and Advanced Mode preserve the same underlying data.
22. Panels collapse without breaking the viewport.
23. The interface remains readable in both dark and light environments.
24. No buttons are inert.
25. No uncaught errors appear during normal use.
26. The application version is visible.
27. Autosave state is visible.
28. The application works without telemetry or an account.
29. The primary experience works offline.
30. The final result feels like a finished creative instrument rather than a technical demonstration.

---

## 26. DELIVERABLES

Deliver:

- Complete working application
- All HTML, CSS, JavaScript, and local dependencies
- Visible version number
- README
- Keyboard shortcut guide
- Project schema documentation
- Sample project files
- Several editable world presets
- Clear instructions for static hosting
- No placeholder controls
- No mock-only features
- No required backend

The final product should make it easy to generate a compelling world immediately while providing enough depth for users to create intricate, evolving ASCII environments and cinematic simulations.