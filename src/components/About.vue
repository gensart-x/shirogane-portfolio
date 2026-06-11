<template>
  <section id="about" class="section about">
    <div class="container">
      <h2 class="about-heading">about</h2>
      <div class="about-grid">
        <div class="about-text">
          <p>
            i design and build software across the stack. focused on
            systems that are maintainable, performant, and actually
            useful. i write code in go, typescript, python, and php,
            and i work with everything from bare metal servers to
            modern edge runtimes.
          </p>
          <p>
            currently exploring distributed systems, automation
            tooling, and self-hosted infrastructure. i believe in
            minimalism in both code and design - ship less, maintain
            less, sleep better.
          </p>
        </div>
        <div class="about-stats">
          <div class="stat">
            <span class="stat-value">5+</span>
            <span class="stat-label">years coding</span>
          </div>
          <div class="stat">
            <span class="stat-value">30+</span>
            <span class="stat-label">repos</span>
          </div>
          <div class="stat">
            <span class="stat-value">full</span>
            <span class="stat-label">stack focus</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  border-top: 1px solid var(--border);
  z-index: 1;
  position: relative;
}

.about-heading {
  font-size: 0.7rem;
  font-weight: 400;
  color: var(--muted);
  letter-spacing: 0.04em;
  margin-bottom: 1.5rem;
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 200px;
  gap: 4rem;
  align-items: start;
}

.about-text {
  font-size: 1rem;
  line-height: 1.7;
  max-width: 65ch;
}

.about-text p {
  margin-bottom: 1.2rem;
  color: var(--fg);
}

.about-stats {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.stat {
  font-family: var(--mono);
}

.stat-value {
  display: block;
  font-size: 1.5rem;
  font-weight: 600;
  line-height: 1;
  margin-bottom: 0.2rem;
}

.stat-label {
  font-size: 0.65rem;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--muted);
}

@media (max-width: 768px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
}
</style>
