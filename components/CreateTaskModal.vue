<template>
  <div v-if="show" class="modal">
    <div class="modal-content">
      <span class="close" @click="closeModal">&times;</span>
      <h2>Buat Tugas Baru</h2>
      <input v-model="newTaskTitle" placeholder="Masukkan judul tugas" />
      <button @click="handleSubmit">Buat</button>
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
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgb(0, 0, 0);
  background-color: rgba(0, 0, 0, 0.4);
}
.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
}
.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}
.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>
