<template>
  <div class="section-editor ">
    <h2>Editor de Sección</h2>
    <input v-model="localSection.title" placeholder="Título de la sección" class="input" />
    <textarea v-model="localSection.content" rows="10" placeholder="Contenido..." class="input"></textarea>
    <button @click="save" class="save-button">Guardar sección</button>
  </div>
</template>

<script setup>
import { watch, reactive } from 'vue'

const props = defineProps(['currentSection'])
const emit = defineEmits(['save'])

const localSection = reactive({
  title: '',
  content: '',
  index: null
})

watch(
    () => props.currentSection,
    (newVal) => {
      Object.assign(localSection, newVal)
    },
    {immediate: true}
)

function save() {
  emit('save', {...localSection})
}
</script>

<style scoped>
.section-editor {
  background-color: rgba(17, 17, 17, 0.47);
  color: #39ff14;
  padding: 16px;
  border-radius: 10px;
  box-shadow: 0 0 10px #39ff14;
  display: flex;
  flex-direction: column;
  font-family: monospace;
}

.input {
  width: 100%;
  box-sizing: border-box;
  background-color: #000;
  color: #39ff14;
  border: 1px solid #39ff14;
  padding: 8px;
  border-radius: 6px;
  margin-bottom: 12px;
  font-family: monospace;
}

.input::placeholder {
  color: #888;
}

h2 {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 12px;
}

.save-button {
  background-color: #39ff14;
  color: #000;
  font-weight: bold;
  padding: 10px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-family: monospace;
}

.save-button:hover {
  background-color: #66ff66;
}
</style>
