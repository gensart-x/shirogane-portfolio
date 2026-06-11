<template>
  <header class="nav">
    <div class="container nav-inner">
      <a href="#top" class="nav-brand mono">gensart</a>
      <nav class="nav-links">
        <a href="#work" class="link-underline">work</a>
        <a href="#about" class="link-underline">about</a>
        <a href="#contact" class="link-underline">contact</a>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.nav {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--bg);
  border-bottom: 1px solid var(--border);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}

.nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 56px;
}

.nav-brand {
  font-size: 0.85rem;
  font-weight: 600;
  letter-spacing: 0.02em;
}

.nav-links {
  display: flex;
  gap: 1.5rem;
  font-family: var(--mono);
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

@media (max-width: 640px) {
  .nav-links {
    gap: 1rem;
    font-size: 0.7rem;
  }
}
</style>
