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
  <section class="section interests-section" aria-labelledby="interests-heading">
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
        <h2 id="interests-heading" class="section-title">{{ data.title }}</h2>
      </div>
      <button
        type="button"
        class="toggle-btn"
        :aria-label="isOpen ? '收起學習興趣' : '展開學習興趣'"
        @click.stop="toggle"
      >
        <span class="toggle-text">{{ isOpen ? '收起' : '展開' }}</span>
        <span class="toggle-icon" :class="{ 'is-collapsed': !isOpen }">▼</span>
      </button>
    </div>

    <div class="collapse-wrapper" :class="{ 'is-open': isOpen }">
      <div class="collapse-inner">
        <div class="section-content">
          <div class="grid-cards">
            <article v-for="item in data.items" :key="item.id" class="card">
              <h3 class="card-title">{{ item.title }}</h3>
              <p class="card-desc">{{ item.desc }}</p>
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

.grid-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 16px;
}

.card {
  background: linear-gradient(180deg, #fdfbf7 0%, #f7f2e6 100%);
  border: 1px solid var(--color-border);
  border-left: 4px solid var(--color-primary);
  border-radius: 4px;
  padding: 18px;
  transition: var(--transition-smooth);
  position: relative;
}

.card:hover {
  border-color: var(--color-gold);
  border-left-color: var(--color-accent);
  box-shadow: 
    0 6px 16px rgba(10, 27, 51, 0.12),
    0 0 0 1px rgba(197, 147, 54, 0.2);
  transform: translateY(-2px);
  background: #fdfaf3;
}

.card-title {
  font-family: var(--font-family-serif);
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--color-primary-dark);
  margin-bottom: 8px;
  line-height: 1.4;
}

.card-desc {
  font-size: 0.92rem;
  color: var(--color-text-muted);
  line-height: 1.75;
  margin-bottom: 0;
  overflow-wrap: break-word;
  word-break: break-all;
}

@media (max-width: 600px) {
  .grid-cards {
    grid-template-columns: 1fr;
    gap: 12px;
  }

  .card {
    padding: 14px;
  }
}
</style>
