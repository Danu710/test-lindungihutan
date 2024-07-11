<template>
  <div v-if="show" class="modal">
    <div class="modal-overlay" @click="closeModal"></div>
    <div class="modal-content">
      <span class="close" @click="closeModal">&times;</span>
      <h2>Buat Tugas Baru</h2>
      <input
        v-model="newTaskTitle"
        placeholder="Masukkan judul tugas"
        class="input-field" />
      <button @click="handleSubmit" class="btn-create">Buat</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { defineEmits } from 'vue';

const props = defineProps({
  show: Boolean,
});

const newTaskTitle = ref('');
const emit = defineEmits(['create', 'close']);

const closeModal = () => {
  emit('close');
};

const handleSubmit = () => {
  emit('create', newTaskTitle.value);
  newTaskTitle.value = '';
  closeModal();
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  max-width: 400px;
  width: 100%;
  max-height: 80%;
  overflow: auto;
  position: relative;
}

.close {
  position: absolute;
  top: 10px;
  right: 10px;
  cursor: pointer;
  font-size: 1.5rem;
  color: #888;
}

h2 {
  margin-top: 0;
  font-size: 1.5rem;
}

.input-field {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.btn-create {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 30px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn-create:hover {
  background-color: #45a049;
}
</style>
