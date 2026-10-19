<script setup>
import { reactive, computed } from 'vue'
import { profileData } from '@/data/profileData'
import ProfileHeader from './components/ProfileHeader.vue'
import AboutSection from './components/AboutSection.vue'
import InterestsSection from './components/InterestsSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ProfileFooter from './components/ProfileFooter.vue'

const sections = reactive({
  about: true,
  interests: true,
  skills: true,
  projects: true
})

const allExpanded = computed(() => Object.values(sections).every(Boolean))
const allCollapsed = computed(() => Object.values(sections).every(v => !v))

function setAllSections(expand = true) {
  Object.keys(sections).forEach(key => {
    sections[key] = expand
  })
}
</script>

<template>
  <div class="container">
    <ProfileHeader :data="profileData.header" />

    <!-- 全域快速收合/展開控制列 -->
    <div class="toolbar" aria-label="區塊收合快速控制">
      <button
        type="button"
        class="toolbar-btn"
        :disabled="allExpanded"
        @click="setAllSections(true)"
        title="展開所有區塊"
      >
        <span class="toolbar-icon">＋</span> 全部展開
      </button>
      <button
        type="button"
        class="toolbar-btn"
        :disabled="allCollapsed"
        @click="setAllSections(false)"
        title="收起所有區塊"
      >
        <span class="toolbar-icon">－</span> 全部收起
      </button>
    </div>

    <main class="profile-main">
      <AboutSection
        v-model:open="sections.about"
        :data="profileData.about"
      />
      <InterestsSection
        v-model:open="sections.interests"
        :data="profileData.interests"
      />
      <SkillsSection
        v-model:open="sections.skills"
        :data="profileData.skills"
      />
      <ProjectsSection
        v-model:open="sections.projects"
        :data="profileData.projects"
      />
    </main>

    <ProfileFooter :data="profileData.footer" />
  </div>
</template>
