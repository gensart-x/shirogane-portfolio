<template>
  <section id="screenshots" class="section screenshots">
    <div class="container">
      <h2 class="screenshots-heading mono">album</h2>
      <div v-if="images.length" class="screenshots-grid">
        <button
          v-for="(img, i) in images"
          :key="i"
          class="screenshots-thumb"
          @click="open(i)"
        >
          <img :src="img.thumb" :alt="img.alt" loading="lazy" />
        </button>
      </div>
      <p v-else class="mono screenshots-empty">no screenshots yet — add images to <code>public/images/work/</code></p>
    </div>

    <Teleport to="body">
      <Transition name="modal">
        <div
          v-if="activeIndex !== null"
          class="screenshots-overlay"
          tabindex="0"
          ref="albumRef"
          @keydown.escape="close"
          @keydown.left="prev"
          @keydown.right="next"
          @click.self="close"
        >
          <button class="screenshots-close" @click="close" aria-label="close">✕</button>
          <button v-if="activeIndex > 0" class="screenshots-nav screenshots-prev" @click="prev" aria-label="previous">←</button>
          <button v-if="activeIndex < images.length - 1" class="screenshots-nav screenshots-next" @click="next" aria-label="next">→</button>
          <img :src="images[activeIndex]?.full" :alt="images[activeIndex]?.alt" class="screenshots-full" />
        </div>
      </Transition>
    </Teleport>
  </section>
</template>

<script setup>
import { ref, nextTick } from 'vue'

const activeIndex = ref(null)
const albumRef = ref(null)

// ponytail: edit these paths when you drop images into public/images/work/
const images = ref([
  { thumb: '/images/work/sample-demon-girl.jpg', full: '/images/work/sample-demon-girl.jpg', alt: 'demon girl with side ponytail and oni horns' },
  { thumb: '/images/work/sample-neko-girl.jpg', full: '/images/work/sample-neko-girl.jpg', alt: 'neko girl reaching out with cat ears' },
])

function open(i) { activeIndex.value = i; nextTick(() => albumRef.value?.focus()) }
function close() { activeIndex.value = null }
function prev() { if (activeIndex.value > 0) activeIndex.value-- }
function next() { if (activeIndex.value < images.value.length - 1) activeIndex.value++ }
</script>

<style scoped>
.screenshots { border-top: 1px solid var(--border); }
.screenshots-heading {
  font-size: 0.7rem; font-weight: 400; color: var(--muted);
  letter-spacing: 0.04em; margin-bottom: 1.5rem;
}
.screenshots-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 0.75rem;
}
.screenshots-thumb {
  all: unset; cursor: pointer; overflow: hidden;
  border: 1px solid var(--border); transition: opacity 0.2s;
}
.screenshots-thumb:hover { opacity: 0.7; }
.screenshots-thumb img {
  display: block; width: 100%; height: 180px;
  object-fit: cover;
}
.screenshots-empty {
  font-size: 0.75rem; color: var(--muted);
  padding: 2rem 0; text-align: center;
}
.screenshots-empty code { font-size: inherit; }

/* overlay/lightbox */
.screenshots-overlay {
  position: fixed; inset: 0; z-index: 1000;
  background: rgba(0,0,0,0.85);
  display: flex; align-items: center; justify-content: center;
}
.screenshots-full {
  max-width: 90vw; max-height: 85vh; object-fit: contain;
  border: 1px solid var(--border);
}
.screenshots-close {
  position: absolute; top: 1rem; right: 1rem;
  background: none; border: none; color: #fff;
  font-size: 1.5rem; cursor: pointer;
  font-family: var(--mono);
}
.screenshots-nav {
  position: absolute; top: 50%; transform: translateY(-50%);
  background: none; border: none; color: #fff;
  font-size: 2rem; cursor: pointer; padding: 0.5rem;
  font-family: var(--mono);
}
.screenshots-prev { left: 0.5rem; }
.screenshots-next { right: 0.5rem; }

.modal-enter-active, .modal-leave-active { transition: opacity 0.2s ease; }
.modal-enter-from, .modal-leave-to { opacity: 0; }
</style>
