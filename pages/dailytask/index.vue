<template>
  <div class="flex flex-col items-center justify-center p-5 m-5">
    <div class="flex items-center justify-start">
      <h1 class="font-mono text-2xl text-black shadow-md">Pages Daily Task</h1>
      <button @click="openModal">Buat Tugas Baru</button>
      <CreateTaskModal
        :show="showModal"
        @close="closeModal"
        @create="createTask" />
    </div>
    <div>
      <ul>
        <li
          v-for="task in tasks"
          :key="task.id"
          :class="{ completed: task.completed }">
          <span @click="toggleTaskCompletion(task.id)">{{ task.title }}</span>
          <button @click="removeTask(task.id)">Hapus</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

interface Task {
  id: number;
  title: string;
  completed: boolean;
}

const tasks = ref<Task[]>([]);
const showModal = ref(false);

const fetchTasks = async () => {
  const response = await fetch(
    'https://jsonplaceholder.typicode.com/todos?_limit=10',
    {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      },
    }
  );
  tasks.value = await response.json();
};

onMounted(() => {
  fetchTasks();
});

const toggleTaskCompletion = async (id: number) => {
  const task = tasks.value.find((t) => t.id === id);
  if (task) {
    task.completed = !task.completed;
    await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
      method: 'PATCH',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ completed: task.completed }),
    });
  }
};

const removeTask = async (id: number) => {
  await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
    method: 'DELETE',
  });
  tasks.value = tasks.value.filter((t) => t.id !== id);
};

const createTask = async (title: string) => {
  const response = await fetch('https://jsonplaceholder.typicode.com/todos', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      title,
      completed: false,
    }),
  });
  const newTask = await response.json();
  tasks.value.push(newTask);
};

const openModal = () => {
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: gray;
}
button {
  margin-left: 10px;
  background-color: red;
  color: white;
  border: none;
  padding: 5px;
  cursor: pointer;
}
</style>
