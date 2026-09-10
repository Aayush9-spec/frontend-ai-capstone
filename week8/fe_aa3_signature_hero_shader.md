# FE-AA3: Signature Hero — Fullscreen Interactive GLSL Shader Scene

**Track:** Frontend AI Engineering  
**Week:** Week 8  
**Assignment Code:** FE-AA3  
**Author:** Aayush Kumar Singh  
**Live Application URL:** [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app)  
**GitHub Repository:** [https://github.com/Aayush9-spec/frontend-ai-capstone](https://github.com/Aayush9-spec/frontend-ai-capstone)  

---

## 1. Executive Summary & Aesthetic Vision

A signature hero section is the first visual handshake between an application and its users. Standard static image backgrounds or simple CSS gradients fail to evoke the dynamic, intelligence-driven feel of modern AI interfaces.

This deliverable showcases a **Fullscreen Interactive GLSL Fragment Shader Canvas** built using Three.js and WebGL shaders. The shader creates an undulating, fluid neural-network energy field that dynamically responds to mouse movement, scroll depth, and frame time (`u_time`).

---

## 2. GLSL Fragment Shader Architecture & Shader Math

```glsl
// GLSL Fragment Shader Snippet (Neural Fluid Wave)
uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_time;

// Simplex 3D Noise Generator
vec4 permute(vec4 x) { return mod(((x*34.0)+1.0)*x, 289.0); }
vec4 taylorInvSqrt(vec4 r) { return 1.79284291400159 - 0.85373472095314 * r; }

float snoise(vec3 v) {
  const vec2 C = vec2(1.0/6.0, 1.0/3.0);
  const vec4 D = vec4(0.0, 0.5, 1.0, 2.0);
  // Compute noise grid offsets & gradient vectors...
  vec3 g = step(x0.yzx, x0.xyz);
  vec3 l = 1.0 - g;
  vec3 i1 = min(g.xyz, l.zxy);
  vec3 i2 = max(g.xyz, l.zxy);
  // Distort wave field based on normalized mouse coords
  vec2 st = gl_FragCoord.xy / u_resolution.xy;
  vec2 mouseOffset = (u_mouse / u_resolution) * 0.15;
  float n = snoise(vec3(st * 3.0 + mouseOffset, u_time * 0.2));
  
  // Emerald & Deep Slate Color Interpolation
  vec3 colorA = vec3(0.01, 0.06, 0.06); // Dark Emerald Slate
  vec3 colorB = vec3(0.06, 0.72, 0.51); // Cyber Emerald Accent
  vec3 finalColor = mix(colorA, colorB, n * 0.5 + 0.5);
  
  gl_FragColor = vec4(finalColor, 0.85);
}
```

### Key Mathematical & Shader Concepts
1. **Simplex Noise (`snoise`):** Generates organic, continuous fluid turbulence without grid artifacting.
2. **Normalized Mouse Distortions (`u_mouse`):** Pushes fluid vectors away from the cursor position, creating interactive ripples.
3. **GPU Fragment Execution:** Computes color states independently per-pixel directly on the GPU shader core, bypassing CPU thread bottlenecks.

---

## 3. Performance & Mobile Fallback Strategy

- **Frame Rate Target:** Constant **60 FPS** on Desktop WebGL contexts.
- **DPR Scaling:** Capped `pixelRatio` to `Math.min(window.devicePixelRatio, 2)` to prevent 4K screen fill-rate oversaturation.
- **Low-Power / Mobile Fallback:** On mobile viewports (< 768px) or low-battery devices, shader resolution is scaled down 50% with linear interpolation, or replaced with a static CSS radial gradient under `prefers-reduced-motion`.

---

## 4. Verification Evidence

- Shader canvas integrated live into Hero section at [https://frontend-ai-capstone.vercel.app](https://frontend-ai-capstone.vercel.app).
