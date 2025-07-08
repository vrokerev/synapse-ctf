<template>
  <div class="section-list">
    <h2>Secciones</h2>
    <draggable :list="sections" @end="onDragEnd" item-key="title">
      <template #item="{ element, index }">
        <div class="section-item">
          <span @click="edit(index)" class="section-title">{{ element.title }}</span>
          <button @click="remove(index)" class="delete-button">🗑️</button>
        </div>
      </template>
    </draggable>
  </div>
</template>

<script setup>
import draggable from 'vuedraggable'

const props = defineProps(['sections'])
const emit = defineEmits(['edit', 'delete', 'reorder'])

function edit(index) {
  emit('edit', index)
}

function remove(index) {
  emit('delete', index)
}

function onDragEnd(evt) {
  emit('reorder', props.sections)
}
</script>

<style scoped>
.section-list {
  background-color: rgba(17, 17, 17, 0.47);
  color: #39ff14;
  padding: 16px;
  border-radius: 10px;
  box-shadow: 0 0 10px #39ff14;
  font-family: monospace;
}

h2 {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 12px;
}

.section-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #000;
  border: 1px solid #39ff14;
  color: #39ff14;
  padding: 8px 12px;
  border-radius: 6px;
  margin-bottom: 10px;
}

.section-title {
  cursor: pointer;
  text-decoration: none;
}

.section-title:hover {
  text-decoration: underline;
}

.delete-button {
  background: none;
  border: none;
  color: #ff5555;
  cursor: pointer;
  font-size: 16px;
  transition: color 0.2s ease;
}

.delete-button:hover {
  color: #ff0000;
}
</style>
