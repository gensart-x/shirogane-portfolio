<template>
  <section id="about" class="section about">
    <div class="container">
      <h2 class="about-heading">about</h2>
      <div class="about-grid">
        <div class="about-text">
          <p>
            he writes php and typescript mostly. python too, but they're on a break right now.
            he genuinely loves bun — it's fast, it's modern, it's just a little sharp
            around the edges. think knife that hasn't been fully sharpened yet.
            gets the job done. just watch your fingers.
          </p>
          <p>
            open source is his lifestyle at this point. 34 public repos and counting.
            some useful, some abandoned, all of them loved at least once.
            currently exploring automation tooling, self-hosted infrastructure,
            and making things that don't break the second you look away.
          </p>
        </div>
        <div class="about-stats">
          <div class="stat">
            <span class="stat-value">34</span>
            <span class="stat-label">public repos</span>
          </div>
          <div class="stat">
            <span class="stat-value">4+</span>
            <span class="stat-label">yrs active</span>
          </div>
          <div class="stat">
            <span class="stat-value">∞</span>
            <span class="stat-label">curiosity</span>
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
