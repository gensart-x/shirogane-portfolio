<template>
  <canvas ref="canvasRef" class="grid-canvas" aria-hidden="true"></canvas>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const canvasRef = ref(null)
let animId = null
let offset = 0
const SPEED = 0.32 // pixels per frame, very subtle
const GAP = 40      // grid cell size in px
const COLORS = { light: { line: 'rgba(0,0,0,0.05)', dot: 'rgba(0,0,0,0.35)' },
                 dark:  { line: 'rgba(255,255,255,0.04)', dot: 'rgba(255,255,255,0.18)' } }

function isDark() {
  return window.matchMedia('(prefers-color-scheme: dark)').matches
}

function resize(c) {
  c.width = window.innerWidth
  c.height = window.innerHeight
}

function draw(c, ctx) {
  const w = c.width
  const h = c.height
  const theme = isDark() ? COLORS.dark : COLORS.light

  ctx.clearRect(0, 0, w, h)
  ctx.strokeStyle = theme.line
  ctx.lineWidth = 1

  // vertical lines
  offset = (offset + SPEED) % GAP
  for (let x = -GAP + offset; x < w + GAP; x += GAP) {
    ctx.beginPath()
    ctx.moveTo(x, 0)
    ctx.lineTo(x, h)
    ctx.stroke()
  }

  // horizontal lines
  for (let y = -GAP; y < h + GAP; y += GAP) {
    ctx.beginPath()
    ctx.moveTo(0, y)
    ctx.lineTo(w, y)
    ctx.stroke()
  }

  // intersection dots
  ctx.fillStyle = theme.dot
  for (let x = -GAP + offset; x < w + GAP; x += GAP) {
    for (let y = 0; y < h + GAP; y += GAP) {
      ctx.beginPath()
      ctx.arc(x, y, 1, 0, Math.PI * 2)
      ctx.fill()
    }
  }
}

onMounted(() => {
  const c = canvasRef.value
  const ctx = c.getContext('2d')
  resize(c)
  window.addEventListener('resize', () => resize(c))

  const reduce = window.matchMedia('(prefers-reduced-motion: reduce)')
  function loop() {
    if (!reduce.matches) draw(c, ctx)
    animId = requestAnimationFrame(loop)
  }
  if (reduce.matches) {
    // draw once, static
    draw(c, ctx)
  } else {
    loop()
  }

  reduce.addEventListener('change', () => {
    if (reduce.matches && animId) {
      cancelAnimationFrame(animId)
      animId = null
      draw(c, ctx)
    } else if (!reduce.matches && !animId) {
      loop()
    }
  })

  c._cleanup = () => {
    window.removeEventListener('resize', () => resize(c))
    if (animId) cancelAnimationFrame(animId)
  }
})

onUnmounted(() => {
  if (canvasRef.value?._cleanup) canvasRef.value._cleanup()
})
</script>

<style scoped>
.grid-canvas {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}
</style>
