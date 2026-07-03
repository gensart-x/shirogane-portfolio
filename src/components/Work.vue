<template>
  <section id="work" class="section work">
    <div class="container">
      <h2 class="work-heading">work</h2>
      <div class="work-list">
        <a v-for="(item, i) in projects" :key="i" :href="item.url || '#'" :target="item.url ? '_blank' : undefined" :rel="item.url ? 'noopener' : undefined" class="work-item" :class="{ 'work-item--featured': item.featured }" @click="handleClick(item, $event)">
          <div class="work-header">
            <span class="mono work-year">{{ item.year }}</span>
            <h3 class="work-name">{{ item.name }}</h3>
            <span v-if="item.status" class="mono work-status">{{ item.status }}</span>
          </div>
          <p class="work-desc">{{ item.desc }}</p>
          <div class="work-meta">
            <span v-for="tag in item.tags" :key="tag" class="mono work-tag">{{ tag }}</span>
          </div>
        </a>
      </div>
    </div>
    <Transition name="toast">
      <div v-if="showToast" class="toast">{{ toastMessage }}</div>
    </Transition>

    <Teleport to="body">
      <Transition name="modal">
        <div
          v-if="galleryIndex !== null"
          class="gallery-overlay"
          tabindex="0"
          @keydown.escape="closeGallery"
          @click.self="closeGallery"
        >
          <button class="gallery-close" @click="closeGallery" aria-label="close">✕</button>
          <button v-if="galleryIndex > 0" class="gallery-nav gallery-prev" @click="prevImg" aria-label="previous">←</button>
          <button v-if="galleryIndex < galleryImages.length - 1" class="gallery-nav gallery-next" @click="nextImg" aria-label="next">→</button>
          <img :src="galleryImages[galleryIndex]" alt="" class="gallery-full" />
        </div>
      </Transition>
    </Teleport>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const showToast = ref(false)
const toastMessage = ref('')

// ── per-work gallery state ──
const galleryIndex = ref(null)
const galleryImages = ref([])

function closeGallery() { galleryIndex.value = null; galleryImages.value = [] }
function prevImg() { if (galleryIndex.value > 0) galleryIndex.value-- }
function nextImg() { if (galleryIndex.value < galleryImages.value.length - 1) galleryIndex.value++ }

function handleClick(item, e) {
  if (item.images?.length) {
    e.preventDefault()
    galleryImages.value = item.images
    galleryIndex.value = 0
    return
  }
  if (item.url) return
  e.preventDefault()
  toastMessage.value = `${item.name} is still cooking. come back later, yeah? 🍳`
  showToast.value = true
  setTimeout(() => { showToast.value = false }, 3500)
}

const projects = [
  {
    year: '2026',
    name: 'eosu (エオス)',
    status: '🚧 in progress',
    desc: "unofficial multi-number WhatsApp gateway. looks like he's trying to clone Fonnte? who knows.",
    url: '',
    tags: ['bun', 'elysia', 'whatsapp-web.js'],
    featured: false,
    images: [
      '/images/work/sample-demon-girl.jpg',
      '/images/work/sample-neko-girl.jpg',
    ],
  },
  {
    year: '2026',
    name: 'shirogane-portfolio',
    status: '✅ shipped',
    desc: "this page. well, not hurt to add my own work too, isn't it, haha.",
    url: 'https://github.com/gensart-x/shirogane-portfolio',
    tags: ['bun', 'vue'],
    featured: true,
    images: [],
  },
  {
    year: '2024',
    name: 'sora-erlyana',
    status: '✅ shipped',
    desc: 'WhatsApp bot with daily useful and funny features. he built it under Node.js and whatsapp-web.js. does what it says on the tin.',
    url: 'https://github.com/gensart-x/sora-erlyana',
    tags: ['node.js', 'express', 'whatsapp-web.js'],
    featured: true,
    images: [],
  },
]
</script>

<style scoped>
.work {
  border-top: 1px solid var(--border);
  z-index: 1;
  position: relative;
}

.work-heading {
  font-size: 0.7rem;
  font-weight: 400;
  color: var(--muted);
  letter-spacing: 0.04em;
  margin-bottom: 1.5rem;
}

.work-list {
  display: flex;
  flex-direction: column;
  gap: 0;
}

.work-item {
  display: block;
  padding: 1.5rem 0;
  border-bottom: 1px solid var(--border);
  transition: opacity 0.2s ease;
  cursor: pointer;
}

.work-item:hover {
  opacity: 0.7;
}

.work-item--featured {
  border-left: 2px solid var(--fg);
  padding-left: 1rem;
  margin-left: -1rem;
}

.work-header {
  display: flex;
  align-items: baseline;
  gap: 1rem;
  margin-bottom: 0.3rem;
  flex-wrap: wrap;
}

.work-year {
  font-size: 0.65rem;
  color: var(--muted);
  white-space: nowrap;
}

.work-name {
  font-size: 1.1rem;
  font-weight: 600;
}

.work-status {
  font-size: 0.6rem;
  color: var(--muted);
  letter-spacing: 0.04em;
}

.work-desc {
  font-size: 0.85rem;
  color: var(--muted);
  line-height: 1.5;
  margin-bottom: 0.5rem;
  max-width: 65ch;
}

.work-meta {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.work-tag {
  font-size: 0.6rem;
  padding: 0.15rem 0.4rem;
  border: 1px solid var(--border);
  color: var(--muted);
  letter-spacing: 0.04em;
}

.toast {
  position: fixed;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  background: var(--fg);
  color: var(--bg);
  font-family: var(--mono);
  font-size: 0.7rem;
  padding: 0.75rem 1.2rem;
  border-radius: 8px;
  z-index: 999;
  text-align: center;
  line-height: 1.5;
  max-width: calc(100vw - 2rem);
  letter-spacing: 0.02em;
}

.toast-enter-active,
.toast-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.toast-enter-from {
  opacity: 0;
  transform: translateX(-50%) translateY(12px);
}

.toast-leave-to {
  opacity: 0;
  transform: translateX(-50%) translateY(12px);
}

/* gallery overlay */
.gallery-overlay {
  position: fixed; inset: 0; z-index: 1000;
  background: rgba(0,0,0,0.85);
  display: flex; align-items: center; justify-content: center;
}
.gallery-full {
  max-width: 90vw; max-height: 85vh; object-fit: contain;
  border: 1px solid var(--border);
}
.gallery-close {
  position: absolute; top: 1rem; right: 1rem;
  background: none; border: none; color: #fff;
  font-size: 1.5rem; cursor: pointer;
  font-family: var(--mono);
}
.gallery-nav {
  position: absolute; top: 50%; transform: translateY(-50%);
  background: none; border: none; color: #fff;
  font-size: 2rem; cursor: pointer; padding: 0.5rem;
  font-family: var(--mono);
}
.gallery-prev { left: 0.5rem; }
.gallery-next { right: 0.5rem; }

.modal-enter-active, .modal-leave-active { transition: opacity 0.2s ease; }
.modal-enter-from, .modal-leave-to { opacity: 0; }
</style>
