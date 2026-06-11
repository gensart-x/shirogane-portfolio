<template>
  <section id="work" class="section work">
    <div class="container">
      <h2 class="work-heading">work</h2>
      <div class="work-list">
        <a v-for="(item, i) in projects" :key="i"
           :href="item.url"
           target="_blank" rel="noopener"
           class="work-item"
           :class="{ 'work-item--featured': item.featured }">
          <div class="work-header">
            <span class="mono work-year">{{ item.year }}</span>
            <h3 class="work-name">{{ item.name }}</h3>
          </div>
          <p class="work-desc">{{ item.desc }}</p>
          <div class="work-meta">
            <span v-for="tag in item.tags" :key="tag" class="mono work-tag">{{ tag }}</span>
          </div>
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
const projects = [
  {
    year: '2026',
    name: 'sora-erlyana',
    desc: 'A modular Discord bot with plugin architecture, built-in moderation, music playback, and AI-powered conversation features.',
    url: 'https://github.com/gensart-x/sora-erlyana',
    tags: ['typescript', 'discord.js', 'openai'],
    featured: true,
  },
  {
    year: '2026',
    name: 'wa-gateway',
    desc: 'Self-hosted WhatsApp gateway server using Baileys and Elysia on Bun. Minimalist dashboard with real-time QR auth.',
    url: 'https://kanialater.insomnia247.nl',
    tags: ['bun', 'baileys', 'elysia'],
    featured: true,
  },
  {
    year: '2025',
    name: 'review-later',
    desc: 'Password-protected file browser and asset server for personal use. Built for self-hosted media workflows.',
    url: '#',
    tags: ['python', 'flask', 'self-hosted'],
  },
  {
    year: '2025',
    name: 'insomnia247',
    desc: 'Server management toolkit for automating vhost configuration, MySQL databases, and SSL certificates.',
    url: '#',
    tags: ['ruby', 'cli', 'devops'],
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
</style>
