# HyperFrames: HTML-to-Video Rendering Framework

**Source**: https://github.com/heygen-com/hyperframes  
**Developer**: HeyGen  
**Type**: Open-source rendering engine

## What Is HyperFrames?

HyperFrames transforms HTML, CSS, and animations into deterministic MP4 videos. It's an open-source rendering engine that bridges web authoring with video production, enabling developers and AI agents to create video content programmatically.

**Key Principle**: *Write once, render consistently — HTML as a video composition language.*

## Core Purpose

HyperFrames solves the problem of **programmatic video generation** by allowing creators to:
- Write familiar HTML compositions with animations
- Render consistently to video files
- Automate video production workflows
- Eliminate manual video editing

**Ideal for**:
- AI coding agents generating video content
- CI/CD pipelines with video outputs
- Automated marketing/social content
- Data visualization videos
- Product demos and documentation
- Real-time video generation APIs

---

## Key Features

### 1. HTML-Native Authoring
- Write plain HTML with data attributes
- No React, no proprietary formats
- Familiar web technologies (HTML/CSS/JavaScript)
- Easy to integrate into existing workflows

**Example**:
```html
<div class="composition" data-width="1920" data-height="1080">
  <h1 class="title">Product Launch</h1>
  <div class="animation" data-animation="fade-in">
    Content here
  </div>
</div>
```

### 2. Deterministic Rendering
- Identical input always produces identical video output
- No random variations
- Perfect for automated pipelines
- Reproducible across environments

### 3. Animation Support
- GSAP animations (GreenSock Animation Platform)
- CSS keyframe animations
- Lottie animations (Adobe After Effects)
- Three.js 3D graphics
- Custom animation adapters
- Frame-by-frame control

### 4. Component Catalog
Pre-built reusable blocks:
- **Transitions**: Fade, slide, wipe, dissolve
- **Charts**: Data visualization (charts, graphs)
- **Captions**: Text overlays, subtitles, labels
- **Effects**: Blur, brightness, distortion
- **Shapes**: Geometry, gradients, patterns
- **Custom**: Build your own components

### 5. Agent-Friendly Integration
- Integrates with Claude, Cursor, Gemini
- Pre-installed skills for AI agents
- Natural language prompts → video generation
- Hands-off video creation

### 6. Multiple Rendering Options
- **Local CLI**: `hyperframes render`
- **Docker**: Containerized rendering
- **AWS Lambda**: Cloud-based rendering at scale
- **Studio UI**: Browser-based editor with live preview

### 7. Design System Integration
- **frame.md** inverts web design specs for video composition
- Bridge between design and video production
- Maintainable design systems for video

---

## Architecture

HyperFrames uses modular packages:

```
hyperframes/
├── CLI                    - Scaffolding & rendering commands
├── Core Engine           - Headless Chrome + FFmpeg rendering
├── Studio UI             - Browser-based composition editor
├── AWS Lambda            - Cloud rendering infrastructure
├── Component Library     - Pre-built animations & transitions
├── Skill Definitions     - AI agent integration
└── Adapters              - Animation framework connectors
```

### Rendering Pipeline

1. **Input**: HTML composition file
2. **Parse**: Extract structure and animations
3. **Render**: Headless Chrome renders each frame
4. **Encode**: FFmpeg converts frames to MP4
5. **Output**: MP4 video file

---

## Developer Usage

### Setup & Installation

```bash
# Initialize a new project
npx hyperframes init my-video

# Install dependencies
cd my-video
npm install

# Preview in browser (live hot reload)
npm run dev

# Render to MP4
hyperframes render composition.html -o output.mp4

# Render with Docker (no local dependencies needed)
docker run heygen/hyperframes render composition.html
```

### Basic Workflow

```
1. Create composition.html (HTML with animations)
2. Preview with `npm run dev`
3. Iterate on design and animations
4. Render to MP4 with `hyperframes render`
5. Deploy or distribute video
```

### For AI Agents (Claude, Cursor, Gemini)

```
1. Agent reads skill definition for HyperFrames
2. Agent generates HTML composition based on prompt
3. Agent uses CLI to render video
4. Video is created automatically
5. No manual intervention needed
```

---

## Animation Framework Support

### GSAP (GreenSock Animation Platform)
```html
<div class="animation" data-animation="gsap">
  <script>
    gsap.to(".element", { duration: 2, x: 100, opacity: 0.5 });
  </script>
</div>
```

### CSS Keyframes
```css
@keyframes slide-in {
  from { transform: translateX(-100%); }
  to { transform: translateX(0); }
}

.element {
  animation: slide-in 1s ease-in-out;
}
```

### Lottie (Adobe After Effects)
```html
<div data-lottie="animation.json" data-loop="true"></div>
```

### Three.js (3D Graphics)
```html
<div class="three-d-scene" data-animation="three-js">
  <!-- Three.js 3D scene -->
</div>
```

---

## Component Library (Pre-Built)

### Transitions
- Fade in/out
- Slide (left, right, up, down)
- Wipe
- Dissolve
- Blur transition
- Zoom
- Rotate

### Charts & Data Visualization
- Bar charts
- Line graphs
- Pie charts
- Animated counters
- Data-driven animations

### Text & Captions
- Title overlays
- Subtitles
- Credit rolls
- Text animations (typewriter, glow, etc.)
- Multi-language support

### Effects
- Blur
- Brightness/contrast
- Color grading
- Distortion
- Chromatic aberration
- Particle effects

---

## Rendering Options

### Option 1: Local CLI (Recommended for Development)
```bash
hyperframes render composition.html -o video.mp4 --format mp4 --fps 30 --resolution 1920x1080
```

**Pros**: Fast iteration, full control  
**Cons**: Requires local setup, slower for large batches

### Option 2: Docker (Portable)
```bash
docker run -v $(pwd):/work heygen/hyperframes render composition.html -o video.mp4
```

**Pros**: No local dependencies, reproducible across systems  
**Cons**: Slightly slower startup

### Option 3: AWS Lambda (Scalable)
```javascript
const hyperframes = require('@hyperframes/aws');
const video = await hyperframes.render(compositionHTML);
```

**Pros**: Scales automatically, pay-per-use, fast  
**Cons**: Cloud dependency, networking latency

### Option 4: Studio UI (Visual Editing)
- Browser-based editor
- Drag-and-drop components
- Live preview
- Export to MP4
- Suitable for non-technical creators

---

## Use Cases

### 1. AI-Generated Video Content
```
Prompt: "Create a 30-second product demo video"
↓
Claude generates HTML composition
↓
HyperFrames renders to MP4
↓
Video ready to deploy
```

### 2. Data Visualization Videos
```
Data input → HyperFrames charts → Animated video
Great for: Marketing, reports, dashboards
```

### 3. Marketing & Social Content
```
Template + dynamic data → HyperFrames → 100 videos
Perfect for: Campaign variations, personalization
```

### 4. Documentation & Tutorials
```
Code walkthrough → Screen recordings + animations
Use case: Product docs, engineering guides
```

### 5. Live Streaming Integration
```
Real-time data → HyperFrames → Stream overlay
Applications: Sports, finance, gaming
```

---

## Best Practices

### ✓ DO:
- Use data attributes for configuration (easier for AI agents)
- Keep compositions modular (reuse components)
- Test animations in browser before rendering
- Version control composition files
- Use consistent naming conventions
- Document animation timings
- Optimize images before embedding
- Use relative paths for assets

### ✗ DON'T:
- Embed absolute file paths
- Use external network requests (not deterministic)
- Create extremely long videos (chunk instead)
- Embed secret credentials
- Ignore frame rate settings (affects smoothness)
- Render without testing preview
- Use non-deterministic JavaScript (Math.random)
- Forget to test on target resolution

---

## Integration with Public Good App

HyperFrames could be used for:

1. **Campaign Videos**: Auto-generate promotional videos for initiatives
2. **Vote Progress Videos**: Animate vote counts and district progress
3. **Impact Visualizations**: Create videos showing greenery impact (before/after)
4. **Educational Content**: Video tutorials on how to use the app
5. **Social Media**: Auto-generate shareable video content from vote data

**Example**:
```
Vote data → HyperFrames composition → "Vote for more trees!" video
Share on social → Drive engagement
```

---

## Key Resources

- **GitHub**: https://github.com/heygen-com/hyperframes
- **Documentation**: In repository README
- **CLI**: `npx hyperframes`
- **Component Gallery**: Pre-built animations and transitions
- **Agent Skills**: Integration with Claude, Cursor, Gemini

---

## Comparison: HyperFrames vs. Alternatives

| Feature | HyperFrames | FFmpeg | MoviePy | Remotion |
|---------|------------|--------|---------|----------|
| **HTML-native** | ✓ Yes | ✗ No | ✗ No | ✓ Yes (React) |
| **Agent-friendly** | ✓ Yes | ✗ No | ✗ No | ~ Partial |
| **Deterministic** | ✓ Yes | ✓ Yes | ✗ No | ✓ Yes |
| **Animation support** | ✓ GSAP, CSS, Lottie, Three.js | ✗ Limited | ~ Basic | ✓ React-based |
| **Cloud rendering** | ✓ Lambda | ~ Possible | ~ Possible | ✓ Yes |
| **Learning curve** | Easy (HTML) | Hard (CLI) | Medium (Python) | Medium (React) |

---

## Summary: HyperFrames Framework

HyperFrames is a **deterministic HTML-to-video rendering engine**:

1. **Write** HTML compositions with animations
2. **Preview** in browser with hot reload
3. **Render** to MP4 (local, Docker, or Lambda)
4. **Automate** with AI agents (Claude, Cursor, Gemini)
5. **Scale** using cloud infrastructure

**Core Mindset**: HTML as a video composition language, deterministic rendering, AI-friendly automation

For the Public Good app: Use HyperFrames to auto-generate campaign videos, progress visualizations, and social media content from vote data.
