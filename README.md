# Adam Khalil · Frontend

I build websites with Vue, motion and WebGL, from design to deploy. I also run Caowl Studios, a web studio in Stockholm.

This repo shows selected work. The source code for each project lives in its own private repo, so here you'll find screenshots, a live link and notes on what I built and why.

---

## Balansio Redovisning

**Live:** [balansio.se](https://balansio.se)

<p>
  <img src="images/balansio-desktop.jpg" alt="Balansio website on desktop" width="68%">
  &nbsp;
  <img src="images/balansio-mobile.jpg" alt="Balansio website on mobile" width="26%">
</p>

Website for an accounting firm in Stockholm. I did the whole project myself: design, frontend, animation and deployment.

### What I built

- A Vue 3 single-page app built with Vite, with one component per section and scoped styles
- A hero background drawn by a custom fragment shader on WebGL2
- Scroll-driven animation with GSAP and ScrollTrigger, and smooth scrolling with Lenis
- A drawer navigation built from scratch, which turns off its motion when the user has `prefers-reduced-motion` set
- A layout that works from 375 px phones up to wide desktop screens
- Self-hosted Inter Variable font, so no requests go to a third-party font service

### Frontend decision: OGL instead of Three.js for the shader

The hero background is one full-screen plane with a fragment shader on it. Three.js would have worked, but its scene graph, materials and loaders would mostly go unused for a single plane. I used [OGL](https://github.com/oframe/ogl) instead, a small WebGL library that gives me the renderer and the shader program without the rest.

A shader that runs all the time drains battery on phones, so the render loop only runs when it's needed:

- It stops when the hero scrolls out of view (`IntersectionObserver`)
- It stops when the browser tab is hidden (`visibilitychange`)
- The device pixel ratio is capped, so high-density screens don't render more pixels than the effect needs

### Stack

| Area | Tools |
| --- | --- |
| Framework | Vue 3, Vue Router |
| Build | Vite |
| Graphics | OGL (WebGL2), GLSL |
| Animation | GSAP, ScrollTrigger, Lenis |
| Styling | Scoped CSS in Vue components |
| Hosting | one.com, static build |
