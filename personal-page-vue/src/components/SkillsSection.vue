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
  <section class="section skills-section" aria-labelledby="skills-heading">
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
        <h2 id="skills-heading" class="section-title">{{ data.title }}</h2>
      </div>
      <button
        type="button"
        class="toggle-btn"
        :aria-label="isOpen ? '收起技能列表' : '展開技能列表'"
        @click.stop="toggle"
      >
        <span class="toggle-text">{{ isOpen ? '收起' : '展開' }}</span>
        <span class="toggle-icon" :class="{ 'is-collapsed': !isOpen }">▼</span>
      </button>
    </div>

    <div class="collapse-wrapper" :class="{ 'is-open': isOpen }">
      <div class="collapse-inner">
        <div class="section-content">
          <div class="skills-group">
            <div
              v-for="cat in data.categories"
              :key="cat.id"
              class="skill-category"
            >
              <h3 class="category-title">{{ cat.title }}</h3>
              <ul class="tag-list">
                <li v-for="tag in cat.tags" :key="tag" class="tag">
                  {{ tag }}
                </li>
              </ul>
            </div>
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

.skills-group {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.skill-category {
  padding-bottom: 16px;
  border-bottom: 1px dashed var(--color-border);
}

.skill-category:last-child {
  border-bottom: none;
  padding-bottom: 0;
}

.category-title {
  font-family: var(--font-family-serif);
  font-size: 1rem;
  font-weight: 700;
  color: var(--color-primary-dark);
  margin-bottom: 12px;
}

.tag-list {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  list-style: none;
}

.tag {
  background: linear-gradient(180deg, #edf4f9 0%, #e1ecf5 100%);
  color: var(--color-primary-dark);
  border: 1px solid #b7cfe2;
  font-size: 0.88rem;
  padding: 4px 14px;
  border-radius: 4px;
  letter-spacing: 0.02em;
  font-weight: 500;
  box-shadow: 0 1px 3px rgba(10, 27, 51, 0.05);
  transition: var(--transition-smooth);
  cursor: default;
}

.tag:hover {
  background: var(--color-primary-dark);
  color: #fffaf0;
  border-color: var(--color-primary-dark);
  transform: translateY(-1px);
  box-shadow: 0 4px 10px rgba(10, 27, 51, 0.22);
}

@media (max-width: 600px) {
  .tag {
    font-size: 0.82rem;
    padding: 4px 10px;
  }
}
</style>
