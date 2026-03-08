<script setup>
import { reactive, ref } from 'vue';
import KanbanColumn from './components/KanbanColumn.vue';
import TaskModal from './components/TaskModal.vue';

const board = reactive([
  { 
    id: 1, 
    title: '🚀 Por hacer', 
    color: 'from-indigo-500 to-purple-600', 
    tasks: [] 
  },
  { 
    id: 2, 
    title: '⚡ En progreso', 
    color: 'from-orange-400 to-red-500', 
    tasks: [] 
  },
  { 
    id: 3, 
    title: '✨ Completado', 
    color: 'from-emerald-400 to-cyan-500', 
    tasks: [] 
  }
]);

const isModalOpen = ref(false);
const taskBeingEdited = ref(null);
let currentColumnOfTask = null;

const openModalForTask = ({ task, column }) => {
  taskBeingEdited.value = JSON.parse(JSON.stringify(task));
  currentColumnOfTask = column;
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
  taskBeingEdited.value = null;
  currentColumnOfTask = null;
};

const saveTaskChanges = (updatedTask) => {
  if (!currentColumnOfTask) return;

  const index = currentColumnOfTask.tasks.findIndex(t => t.id === updatedTask.id);

  if (index !== -1) {
    currentColumnOfTask.tasks[index] = updatedTask;
  } else {
    currentColumnOfTask.tasks.push(updatedTask);
  }
  
  closeModal();
};

const deleteTaskFromModal = (taskId) => {
  currentColumnOfTask.tasks = currentColumnOfTask.tasks.filter(t => t.id !== taskId);
  closeModal();
}

const deleteQuickTask = ({ taskId, column }) => {
  column.tasks = column.tasks.filter(t => t.id !== taskId);
};
</script>

<template>
  <div class="h-screen w-full bg-[#0f0f0f] text-[#E3E3E3] flex flex-col font-sans overflow-hidden relative">
    <div class="absolute top-[-10%] left-[-10%] w-[40%] h-[40%] bg-blue-600/10 blur-[120px] rounded-full pointer-events-none"></div>

    <header class="w-full py-6 px-10 border-b border-white/5 shrink-0 bg-[#161616]/50 backdrop-blur-md z-10">
      <h1 class="text-3xl font-black text-center tracking-tighter italic uppercase">
        <span class="bg-clip-text text-transparent bg-linear-to-r from-blue-400 to-purple-500">Gestor</span> de Tareas
      </h1>
    </header>

    <main class="relative z-20 flex-1 overflow-x-auto p-6 md:p-12 no-scrollbar">
      <div class="grid grid-flow-col auto-cols-[350px] gap-8 h-full w-fit mx-auto items-start">
        <KanbanColumn 
          v-for="col in board" 
          :key="col.id" 
          :column="col" 
          @open-modal="openModalForTask"
          @delete-task="deleteQuickTask"
        />
      </div>
    </main>

    <Teleport to="body">
      <TaskModal 
        v-if="isModalOpen"
        :is-open="isModalOpen" 
        :task="taskBeingEdited"
        @close="closeModal"
        @save="saveTaskChanges"
        @delete="deleteTaskFromModal"
      />
    </Teleport>
  </div>
</template>