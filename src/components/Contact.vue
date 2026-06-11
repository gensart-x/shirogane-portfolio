<template>
  <section id="contact" class="section contact">
    <div class="container">
      <h2 class="mono contact-heading">get in touch</h2>
      <p class="contact-desc">
        he's available for freelance, collaboration, or just a good conversation
        about systems and code.
      </p>
      <div class="contact-links">
        <a href="https://github.com/gensart-x" target="_blank" rel="noopener" class="mono contact-link link-underline">
          github
        </a>
        <a href="https://instagram.com/gensart.json" target="_blank" rel="noopener" class="mono contact-link link-underline">
          instagram
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact {
  border-top: 1px solid var(--border);
  z-index: 1;
  position: relative;
}

.contact-heading {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--muted);
  margin-bottom: 1.2rem;
}

.contact-desc {
  font-size: 1rem;
  line-height: 1.6;
  max-width: 50ch;
  margin-bottom: 2rem;
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.contact-link {
  font-size: 0.85rem;
  width: fit-content;
}
</style>
