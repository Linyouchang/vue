<script setup>
const isOpen = defineModel('open', { type: Boolean, default: true })

defineProps({
  data: {
    type: Object,
    required: true
  }
})

function toggle() {
  isOpen.value = !isOpen.value
}
</script>

<template>
  <section class="section projects-section" aria-labelledby="projects-heading">
    <div
      class="section-header"
      :class="{ 'is-collapsed': !isOpen }"
      @click="toggle"
      role="button"
      tabindex="0"
      @keydown.enter.space.prevent="toggle"
      :aria-expanded="isOpen"
    >
      <div class="header-titles">
        <span class="sub-label">{{ data.label }}</span>
        <h2 id="projects-heading" class="section-title">{{ data.title }}</h2>
      </div>
      <button
        type="button"
        class="toggle-btn"
        :aria-label="isOpen ? '收起作品介紹' : '展開作品介紹'"
        @click.stop="toggle"
      >
        <span class="toggle-text">{{ isOpen ? '收起' : '展開' }}</span>
        <span class="toggle-icon" :class="{ 'is-collapsed': !isOpen }">▼</span>
      </button>
    </div>

    <div class="collapse-wrapper" :class="{ 'is-open': isOpen }">
      <div class="collapse-inner">
        <div class="section-content">
          <div class="projects-grid">
            <article
              v-for="project in data.items"
              :key="project.id"
              class="card project-card"
            >
              <a
                :href="project.url"
                target="_blank"
                rel="noopener noreferrer"
                class="project-img-link"
                :aria-label="project.ariaLabel"
              >
                <div class="project-media">
                  <img
                    :src="project.imgSrc"
                    :alt="project.alt"
                    class="project-img"
                    loading="lazy"
                  />
                </div>
              </a>
              <div class="project-info">
                <h3 class="card-title">
                  <a
                    :href="project.url"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="project-title-link"
                  >
                    {{ project.title }}
                  </a>
                </h3>
                <p class="card-desc">
                  <a
                    :href="project.url"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="project-link"
                  >
                    {{ project.url }}
                  </a>
                </p>
              </div>
            </article>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-content {
  padding-top: 2px;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
}

.project-card {
  display: flex;
  flex-direction: column;
  padding: 16px;
  background: linear-gradient(180deg, #fdfbf7 0%, #f5efe3 100%);
  border: 1px solid var(--color-border);
  border-left: 4px solid var(--color-primary);
  border-radius: 4px;
  transition: var(--transition-smooth);
}

.project-card:hover {
  border-color: var(--color-gold);
  border-left-color: var(--color-accent);
  box-shadow: 
    0 8px 20px rgba(10, 27, 51, 0.14),
    0 0 0 1px rgba(197, 147, 54, 0.2);
  transform: translateY(-2px);
}

.project-img-link {
  display: block;
  overflow: hidden;
  border-radius: 3px;
  border: 2px solid var(--color-primary-light);
  margin-bottom: 12px;
  background-color: var(--color-primary-dark);
  text-decoration: none;
  box-shadow: 0 3px 8px rgba(10, 27, 51, 0.15);
  transition: border-color 0.25s ease, box-shadow 0.25s ease;
}

.project-img-link:hover {
  border-color: var(--color-accent);
  box-shadow: 0 4px 12px rgba(192, 54, 34, 0.25);
}

.project-media {
  width: 100%;
  aspect-ratio: 16 / 9;
  overflow: hidden;
}

.project-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.4s cubic-bezier(0.2, 0.8, 0.2, 1), filter 0.4s ease;
}

.project-card:hover .project-img {
  transform: scale(1.04);
}

.project-info {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.card-title {
  font-family: var(--font-family-serif);
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--color-primary-dark);
  margin-bottom: 8px;
  line-height: 1.4;
}

.project-title-link {
  color: var(--color-primary-dark);
  text-decoration: none;
  font-family: var(--font-family-serif);
  font-weight: 700;
  transition: var(--transition-smooth);
}

.project-title-link:hover {
  color: var(--color-accent);
}

.card-desc {
  font-size: 0.92rem;
  color: var(--color-text-muted);
  line-height: 1.75;
  margin-bottom: 0;
  overflow-wrap: break-word;
  word-break: break-all;
}

.project-link {
  color: var(--color-primary);
  text-decoration: underline;
  text-underline-offset: 3.5px;
  text-decoration-color: var(--color-gold);
  transition: var(--transition-smooth);
  word-break: break-all;
  font-size: 0.9rem;
}

.project-link:hover {
  color: var(--color-accent);
  text-decoration-color: var(--color-accent);
}

@media (max-width: 600px) {
  .projects-grid {
    grid-template-columns: 1fr;
    gap: 12px;
  }

  .project-card {
    padding: 14px;
  }
}
</style>
