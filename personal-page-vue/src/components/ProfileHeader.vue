<script setup>
import WaveCrest from './WaveCrest.vue'
import WaveDivider from './WaveDivider.vue'

defineProps({
  data: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <header class="profile-header">
    <WaveCrest />
    <div class="avatar-badge" aria-label="個人標誌">{{ data.avatar }}</div>
    <h1 class="name">{{ data.name }}</h1>
    <p class="tagline">{{ data.tagline }}</p>
    <WaveDivider />
  </header>
</template>

<style scoped>
.profile-header {
  text-align: center;
  padding: 14px 10px 26px;
  position: relative;
}

.avatar-badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 70px;
  height: 70px;
  margin-bottom: 16px;
  background: linear-gradient(135deg, #c73824 0%, #aa2b1a 100%);
  color: #fffaf0;
  font-family: var(--font-family-serif);
  font-size: 34px;
  font-weight: 700;
  border-radius: 10px;
  border: 2px solid #fffaf0;
  box-shadow: 
    0 0 0 3px #c73824,
    0 0 0 5px rgba(18, 51, 92, 0.18),
    0 6px 14px rgba(170, 43, 26, 0.35);
  user-select: none;
  transform: rotate(-2deg);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.avatar-badge:hover {
  transform: rotate(0deg) scale(1.05);
  box-shadow: 
    0 0 0 3px #c73824,
    0 0 0 6px rgba(18, 51, 92, 0.25),
    0 8px 18px rgba(170, 43, 26, 0.45);
}

.name {
  font-family: var(--font-family-serif);
  font-size: 2.25rem;
  font-weight: 700;
  color: var(--color-primary-dark);
  letter-spacing: 0.18em;
  margin-bottom: 8px;
  text-shadow: 
    1px 1px 0 rgba(197, 147, 54, 0.35),
    2px 2px 0 rgba(18, 51, 92, 0.08);
}

.tagline {
  font-size: 0.95rem;
  color: var(--color-text-muted);
  letter-spacing: 0.08em;
  margin-bottom: 22px;
  font-weight: 500;
}

@media (max-width: 600px) {
  .name {
    font-size: 1.75rem;
    letter-spacing: 0.12em;
  }

  .tagline {
    font-size: 0.88rem;
    line-height: 1.5;
  }
}
</style>

