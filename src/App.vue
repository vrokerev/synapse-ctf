<template>
  <div class="app-container min-h-screen w-full bg-black text-neon-green font-mono relative">
    <ParticleBackground />
    <div class="content-wrapper relative z-10 w-full max-w-7xl mx-auto px-2 md:px-6 py-4">
      <h1 class="title text-center mb-6">Synapse CTF</h1>
      <div class="grid-container">
        <div class="column"><InfoForm :info="info" @update="updateInfo" /></div>
        <div class="column"><SectionEditor :currentSection="currentSection" @save="saveSection" /></div>
        <div class="column"><SectionList :sections="sections" @edit="editSection" @delete="deleteSection" @reorder="reorderSections" /></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import InfoForm from './components/InfoForm.vue'
import SectionEditor from './components/SectionEditor.vue'
import SectionList from './components/SectionList.vue'
import ParticleBackground from './components/ParticleBackground.vue'

const info = ref({
  title: '',
  author: '',
  date: new Date().toISOString().split('T')[0],
  difficulty: '',
  customDifficulty: '',
  tags: '',
  os: '',
  customOs: '',
  type: ''
})

const sections = ref([])
const currentSection = ref({title: '', content: '', index: null})

function updateInfo(newInfo) {
  info.value = {...newInfo}
}

function saveSection(section) {
  if (section.index !== null) {
    sections.value[section.index] = {
      title: section.title,
      content: section.content
    }
  } else {
    sections.value.push({
      title: section.title,
      content: section.content
    })
  }
  currentSection.value = {title: '', content: '', index: null}
}

function editSection(index) {
  const section = sections.value[index]
  currentSection.value = {...section, index}
}

function deleteSection(index) {
  sections.value.splice(index, 1)
}

function reorderSections(newOrder) {
  sections.value = newOrder
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&display=swap');

:root {
  --neon-green: #39ff14;
}

.app-container {
  min-height: 100vh;
  background: #000;
  color: var(--neon-green);
  font-family: 'JetBrains Mono', monospace;
}

.title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  text-align: center;
  color: var(--neon-green);
  text-shadow: 0 0 8px #39ff14;
}

.grid-container {
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

@media (min-width: 768px) {
  .grid-container {
    grid-template-columns: 1fr 1fr 1fr;
  }
}

.column {
  min-width: 0;
  display: flex;
  flex-direction: column;
  height: 100%;
}

@media (max-width: 767px) {
  .content-wrapper {
    padding: 0.5rem;
  }
  .title {
    font-size: 2rem;
  }
}
</style>
