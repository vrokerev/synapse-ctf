<template>
  <div class="min-h-screen w-full bg-black text-neon-green font-mono relative overflow-x-hidden flex items-center justify-center">
    <ParticleBackground />
    <div class="relative z-10 w-full max-w-6xl px-4 py-8">
      <h1 class="text-center text-3xl font-bold mb-6">Synapse CTF</h1>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 h-[70vh]">
        <div class="h-full">
          <InfoForm class="h-full" :info="info" @update="updateInfo" />
        </div>
        <div class="h-full">
          <SectionEditor class="h-full" :currentSection="currentSection" @save="saveSection" />
        </div>
        <div class="h-full">
          <SectionList class="h-full"
                       :sections="sections"
                       @edit="editSection"
                       @delete="deleteSection"
                       @reorder="reorderSections"
          />
        </div>
      </div>
    </div>
  </div>
</template>




<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.text-neon-green {
  color: #39ff14;
}

.font-mono {
  font-family: 'Courier New', Courier, monospace;
}

body {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
  background-color: #000;
  color: #39ff14;
}

h1 {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  text-align: center;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
  padding: 0 1rem;
  height: 100%; /* Asegura altura completa en grid */
  align-items: stretch; /* Estira columnas para misma altura */
}

.relative {
  position: relative;
}

.z-10 {
  z-index: 10;
}

</style>




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