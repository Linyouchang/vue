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
  <section class="section about-section" aria-labelledby="about-heading">
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
        <h2 id="about-heading" class="section-title">{{ data.title }}</h2>
      </div>
      <button
        type="button"
        class="toggle-btn"
        :aria-label="isOpen ? '收起自我介紹' : '展開自我介紹'"
        @click.stop="toggle"
      >
        <span class="toggle-text">{{ isOpen ? '收起' : '展開' }}</span>
        <span class="toggle-icon" :class="{ 'is-collapsed': !isOpen }">▼</span>
      </button>
    </div>

    <div class="collapse-wrapper" :class="{ 'is-open': isOpen }">
      <div class="collapse-inner">
        <div class="section-content">
          <p v-for="(paragraph, index) in data.paragraphs" :key="index">
            {{ paragraph }}
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-content {
  padding-top: 2px;
}

.section-content p {
  color: var(--color-text-main);
  margin-bottom: 14px;
  text-align: justify;
}

.section-content p:last-child {
  margin-bottom: 0;
}
</style>
