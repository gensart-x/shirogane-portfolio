<template>
  <GridBg />
  <NavBar />
  <main>
    <Hero />
    <About />
    <Work />
    <Contact />
  </main>
  <footer class="site-footer">
    <p>built with love, maintained with obsession — <a href="https://github.com/gensart-x" target="_blank" class="link-underline mono">Yuno Gasai</a> 💜</p>
    <p class="mono">&copy; 2026 gensart</p>
  </footer>
</template>

<script setup>
import { onMounted } from 'vue'
import GridBg from './components/GridBg.vue'
import NavBar from './components/NavBar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Work from './components/Work.vue'
import Contact from './components/Contact.vue'

onMounted(() => {
  // IntersectionObserver for fade-in reveals
  const els = document.querySelectorAll('.fade-in')
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible')
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.15 }
  )
  els.forEach((el) => observer.observe(el))
})
</script>

<style>
main {
  position: relative;
  z-index: 1;
}

.section {
  padding: 5rem 0;
}

.section-label {
  font-size: 0.65rem;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: var(--muted);
  margin-bottom: 2rem;
}

.site-footer {
  position: relative;
  z-index: 1;
  text-align: center;
  padding: 3rem var(--gap);
  border-top: 1px solid var(--border);
}

.site-footer p {
  font-size: 0.7rem;
  color: var(--muted);
  letter-spacing: 0.05em;
}

.site-footer p.mono {
  font-size: 0.6rem;
  margin-top: 0.4rem;
  opacity: 0.6;
}

.site-footer a {
  color: var(--fg);
}
</style>
