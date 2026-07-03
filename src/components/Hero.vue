<template>
  <section id="top" class="hero">
    <div class="container">
      <div class="hero-content">
        <p class="mono hero-eyebrow fade-in">// software developer</p>
        <h1 class="hero-title fade-in">shipping code<br />that works, mostly.</h1>
        <div class="hero-meta fade-in">
          <span class="mono hero-status"></span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue'

const statusMessages = [
  'fullstack dev',
  'typescript nerd',
  'yandere enthusiast',
  'open source',
  'php never die',
  "don't forget to hate kanokari",
  'rori snatcher 🥅',
]

onMounted(() => {
  const el = document.querySelector('.hero-status')
  if (!el) return
  let i = 0
  function cycle() {
    el.textContent = statusMessages[i % statusMessages.length]
    i++
  }
  cycle()
  const interval = setInterval(cycle, 2200)
  const observer = new MutationObserver(() => {
    if (!document.body.contains(el)) {
      clearInterval(interval)
      observer.disconnect()
    }
  })
  observer.observe(document.body, { childList: true, subtree: true })
})
</script>

<style scoped>
.hero {
  min-height: calc(100dvh - 56px);
  display: flex;
  align-items: center;
  padding-top: 4rem;
  padding-bottom: 4rem;
  position: relative;
  z-index: 1;
}

.hero-content {
  max-width: 680px;
}

.hero-eyebrow {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: var(--muted);
  margin-bottom: 2rem;
}

.hero-title {
  font-size: clamp(2rem, 5vw, 3.5rem);
  font-family: var(--sans);
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.08;
  margin-bottom: 2rem;
}

.hero-meta {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  font-size: 0.72rem;
  color: var(--muted);
  letter-spacing: 0.05em;
  flex-wrap: wrap;
}

.hero-status {
  position: relative;
  padding-left: 1.2em;
}

.hero-status::before {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #22c55e;
  animation: pulse-dot 2s ease-in-out infinite;
}

.hero-sep {
  opacity: 0.4;
}

@keyframes pulse-dot {

  0%,
  100% {
    opacity: 1;
  }

  50% {
    opacity: 0.3;
  }
}

@media (max-width: 640px) {
  .hero {
    padding-top: 3rem;
  }
}
</style>
