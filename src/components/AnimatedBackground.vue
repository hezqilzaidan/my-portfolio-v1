<template>
  <div class="animated-bg" aria-hidden="true">
    <canvas ref="canvasEl" class="bg-canvas"></canvas>
    <div class="bg-overlay"></div>
  </div>
  
</template>

<script>
export default {
  name: 'AnimatedBackground',
  data() {
    return {
      canvasContext: null,
      animationFrameId: null,
      particles: [],
      devicePixelRatio: Math.min(window.devicePixelRatio || 1, 2),
      canvasWidth: 0,
      canvasHeight: 0,
      // Parallax/tilt state
      targetOffsetX: 0,
      targetOffsetY: 0,
      currentOffsetX: 0,
      currentOffsetY: 0,
      lastScrollY: window.scrollY,
      timeStart: performance.now(),
    };
  },
  mounted() {
    this.setupCanvas();
    this.initParticles();
    window.addEventListener('resize', this.onResize, { passive: true });
    window.addEventListener('scroll', this.onScroll, { passive: true });
    this.loop();
  },
  beforeUnmount() {
    cancelAnimationFrame(this.animationFrameId);
    window.removeEventListener('resize', this.onResize);
    window.removeEventListener('scroll', this.onScroll);
  },
  methods: {
    setupCanvas() {
      const canvas = this.$refs.canvasEl;
      const ctx = canvas.getContext('2d');
      this.canvasContext = ctx;

      const rect = canvas.getBoundingClientRect();
      this.canvasWidth = rect.width;
      this.canvasHeight = rect.height;
      const dpr = this.devicePixelRatio;
      canvas.width = Math.floor(this.canvasWidth * dpr);
      canvas.height = Math.floor(this.canvasHeight * dpr);
      ctx.scale(dpr, dpr);
    },
    onResize() {
      // Resize canvas to viewport
      this.setupCanvas();
      // Re-balance number of particles based on area
      this.initParticles();
    },
    onScroll() {
      const y = window.scrollY;
      const delta = y - this.lastScrollY;
      this.lastScrollY = y;
      // Update parallax target based on scroll delta (clamped)
      const clamp = (v, min, max) => Math.max(min, Math.min(max, v));
      this.targetOffsetY = clamp(this.targetOffsetY + delta * 0.15, -80, 80);
      // Add a subtle horizontal sway tied to total scroll
      this.targetOffsetX = clamp((y % 600) - 300, -120, 120) * 0.15;
    },
    initParticles() {
      const area = Math.max(this.canvasWidth * this.canvasHeight, 1);
      const baseCount = Math.round(area / 28000); // density
      const count = Math.min(Math.max(baseCount, 40), 120);

      const newParticles = [];
      for (let i = 0; i < count; i++) {
        newParticles.push(this.createParticle());
      }
      this.particles = newParticles;
    },
    createParticle() {
      // depth gives 3D illusion: size/alpha varies by depth
      const depth = Math.random() * 0.7 + 0.3; // 0.3 - 1.0
      return {
        x: Math.random(), // normalized 0..1
        y: Math.random(), // normalized 0..1
        depth,
        baseSize: Math.random() * 1.6 + 0.8,
        // subtle autonomous drift
        driftX: (Math.random() - 0.5) * 0.05,
        driftY: (Math.random() - 0.5) * 0.05,
        hueShift: Math.random() * 6 - 3,
      };
    },
    updateParticle(p) {
      // time-based drift creating slow motion
      p.x += p.driftX * 0.0008;
      p.y += p.driftY * 0.0008;

      // wrap around edges
      if (p.x < 0) p.x += 1; else if (p.x > 1) p.x -= 1;
      if (p.y < 0) p.y += 1; else if (p.y > 1) p.y -= 1;
    },
    render() {
      const ctx = this.canvasContext;
      if (!ctx) return;
      const w = this.canvasWidth;
      const h = this.canvasHeight;

      // Easing towards target parallax offsets
      this.currentOffsetX += (this.targetOffsetX - this.currentOffsetX) * 0.08;
      this.currentOffsetY += (this.targetOffsetY - this.currentOffsetY) * 0.08;

      // Clear with transparent to allow gradient overlay below
      ctx.clearRect(0, 0, w, h);

      // Slight perspective center
      const centerX = w * 0.5 + this.currentOffsetX;
      const centerY = h * 0.5 + this.currentOffsetY;

      // Draw particles
      for (let i = 0; i < this.particles.length; i++) {
        const p = this.particles[i];
        const px = p.x * w;
        const py = p.y * h;
        const depthScale = p.depth; // 0.3..1 affects size/alpha
        const size = p.baseSize * (1.5 + depthScale * 2);
        const dx = (px - centerX) * (1 - depthScale) * 0.12;
        const dy = (py - centerY) * (1 - depthScale) * 0.12;

        // Soft glow circles
        const gradient = ctx.createRadialGradient(px + dx, py + dy, 0, px + dx, py + dy, size * 2.2);
        // Accent near brand color (#ffdb70) with slight hue variation
        gradient.addColorStop(0, `rgba(255, 219, 112, ${0.18 * depthScale})`);
        gradient.addColorStop(1, 'rgba(255, 219, 112, 0)');

        ctx.fillStyle = gradient;
        ctx.beginPath();
        ctx.arc(px + dx, py + dy, size * 2.2, 0, Math.PI * 2);
        ctx.fill();
      }
    },
    loop() {
      for (let i = 0; i < this.particles.length; i++) {
        this.updateParticle(this.particles[i]);
      }
      this.render();
      this.animationFrameId = requestAnimationFrame(this.loop);
    }
  }
}
</script>

<style>
.animated-bg {
  position: fixed;
  inset: 0;
  z-index: 0; /* keep behind content */
  pointer-events: none; /* do not block UI */
}
.bg-canvas {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}
.bg-overlay {
  position: absolute;
  inset: 0;
  /* Subtle vignette + gradient to add depth */
  background:
    radial-gradient(1200px 600px at 80% 10%, rgba(255, 219, 112, 0.07), rgba(255, 219, 112, 0) 60%),
    radial-gradient(1000px 500px at 10% 90%, rgba(255, 219, 112, 0.06), rgba(255, 219, 112, 0) 60%),
    linear-gradient(180deg, rgba(0,0,0,0.35), rgba(0,0,0,0.15));
}
</style>


