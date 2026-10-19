<script setup>
import WaveDivider from './WaveDivider.vue'

defineProps({
  data: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <footer class="profile-footer">
    <WaveDivider />
    <p class="copyright">{{ data.copyright }}</p>
  </footer>
</template>

<style scoped>
.profile-footer {
  text-align: center;
  padding: 32px 10px 12px;
}

.profile-footer :deep(.divider) {
  margin-bottom: 20px;
}

.copyright {
  font-size: 0.88rem;
  color: var(--color-text-muted);
  letter-spacing: 0.05em;
  margin-bottom: 4px;
}
</style>

