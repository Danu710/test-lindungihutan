<template>
  <div class="flex flex-col items-center justify-center p-5 m-5">
    <div class="flex flex-row justify-between gap-10">
      <h1 class="font-mono text-2xl text-black shadow-md">Pages Daily Task</h1>
      <button @click="openModal" class="btn-create">Buat Tugas Baru</button>
      <CreateTaskModal
        :show="showModal"
        @close="closeModal"
        @create="createTask" />
    </div>
    <div class="pt-10">
      <ul class="task-list">
        <li
          v-for="task in tasks"
          :key="task.id"
          :class="{ completed: task.completed }">
          <span @click="toggleTaskCompletion(task.id)" class="task-title">{{
            task.title
          }}</span>
          <button @click="removeTask(task.id)" class="btn-delete">Hapus</button>
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

.task-list {
  list-style-type: none;
  padding: 0;
}

.task-list li {
  margin-bottom: 10px;
  padding: 10px;
  background-color: #f3f4f6;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-list li.completed {
  background-color: #d1e7dd;
  text-decoration: line-through;
}

.task-title {
  cursor: pointer;
}

.btn-create {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-create:hover {
  background-color: #388e3c;
}

.btn-delete {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-delete:hover {
  background-color: #d32f2f;
}
</style>
