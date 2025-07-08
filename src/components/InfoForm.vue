<template>
  <div class="info-form">
    <h2>Información del Writeup</h2>

    <input v-model="form.title" type="text" placeholder="Título" class="input" />
    <input v-model="form.author" type="text" placeholder="Autor" class="input" />
    <input v-model="form.date" type="date" class="input" />

    <select v-model="form.difficulty" class="input">
      <option disabled value="">Dificultad</option>
      <option>Fácil</option>
      <option>Medio</option>
      <option>Difícil</option>
      <option>Insane</option>
      <option>Otra</option>
    </select>
    <input v-if="form.difficulty === 'Otra'" v-model="form.customDifficulty" placeholder="Dificultad personalizada" class="input" />

    <input v-model="form.tags" type="text" placeholder="Tags (separadas por coma)" class="input" />

    <select v-model="form.os" class="input">
      <option disabled value="">Sistema Operativo</option>
      <option>Windows</option>
      <option>Linux</option>
      <option>MacOS</option>
      <option>Otro</option>
    </select>
    <input v-if="form.os === 'Otro'" v-model="form.customOs" placeholder="Sistema operativo personalizado" class="input" />

    <select v-model="form.type" class="input">
      <option disabled value="">Tipo</option>
      <option>Web</option>
      <option>Pwn</option>
      <option>Crypto</option>
      <option>Forense</option>
      <option>Reversing</option>
    </select>
  </div>
</template>

<script setup>
import { reactive, watch } from 'vue'

const props = defineProps(['info'])
const emit = defineEmits(['update'])

const form = reactive({ ...props.info })

watch(form, () => {
  emit('update', { ...form })
})
</script>

<style scoped>
.info-form {
  background-color: rgba(17, 17, 17, 0.47);
  color: #39ff14;
  padding: 16px;
  border-radius: 10px;
  font-family: monospace;
  box-shadow: 0 0 10px #39ff14;
}

.input {
  display: block;
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
</style>
