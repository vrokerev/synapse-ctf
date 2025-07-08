<template>
  <div class="app-container">
    <ParticleBackground />
    <div class="content-wrapper">
      <h1 class="title">Synapse CTF</h1>
      <div class="columns-wrapper">
        <div class="column">
          <InfoForm :info="info" @update="updateInfo" />
        </div>
        <div class="column">
          <SectionEditor :currentSection="currentSection" @save="saveSection" />
        </div>
        <div class="column">
          <SectionList
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





<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.columns-wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  height: 100vh;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  align-items: stretch;
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
}

.relative {
  position: relative;
}

.z-10 {
  z-index: 10;
}

.column {
  height: 70vh;
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
