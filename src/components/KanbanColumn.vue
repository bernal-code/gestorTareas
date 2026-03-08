<script setup>
import draggable from 'vuedraggable';
import TaskCard from './TaskCard.vue';
  
const props = defineProps(['column']);
const emit = defineEmits(['open-modal', 'delete-task']);
  
const prepareNewTask = () => {
    const newTask = {
        id: Date.now().toString(),
        content: '',
        description: ''
    };
    emit('open-modal', { task: newTask, column: props.column });
};
</script>

<template>
  <div class="w-[350px] z-30 bg-[#1a1a1a]/80 backdrop-blur-xl border border-white/5 rounded-3xl flex flex-col h-full max-h-[85vh] shrink-0 shadow-2xl relative">
    
    <div :class="['h-2 w-full bg-linear-to-r rounded-t-3xl shrink-0', column.color]"></div>

    <div class="p-6 flex flex-col h-full overflow-visible"> 
      <div class="flex items-center justify-between mb-6 shrink-0">
          <span :class="['text-sm font-black uppercase tracking-[0.2em] bg-clip-text text-transparent bg-linear-to-r', column.color]">
            {{ column.title }}
          </span>
          <span class="text-[10px] font-mono text-white/30 bg-white/5 px-2 py-0.5 rounded-full border border-white/5">
            {{ column.tasks.length }}
          </span>
      </div>

      <draggable
        v-model="column.tasks"
        group="tasks"
        item-key="id"
        :animation="200"
        :fallback-tolerance="3"
        class="flex-1 space-y-4 overflow-y-auto overflow-x-visible pr-2 min-h-[500px] pb-40 no-scrollbar" 
        ghost-class="sortable-ghost"
        drag-class="sortable-drag"
      >
        <template #item="{ element }">
          <div class="pb-1"> <TaskCard 
              :task="element" 
              :columnColor="column.color"
              @click="$emit('open-modal', { task: element, column })" 
              @quick-delete="(taskId) => $emit('delete-task', { taskId, column })"
            />
          </div>
        </template>
      </draggable>

      <button 
        @click="prepareNewTask" 
        class="group mt-4 flex items-center gap-3 px-4 py-3 text-gray-400 hover:text-white rounded-xl transition-all duration-300 border border-white/5 hover:border-white/20 hover:bg-white/5 w-full text-left active:scale-95 shrink-0"
      >
        <span :class="['flex items-center justify-center w-8 h-8 rounded-lg bg-linear-to-br shadow-lg opacity-70 group-hover:opacity-100 group-hover:scale-110 transition-all', column.color]">
          <span class="text-white text-xl font-bold">+</span>
        </span>
        <span class="font-bold tracking-tight group-hover:translate-x-1 transition-transform uppercase text-xs">
          Nueva Tarea
        </span>
      </button>
    </div>
  </div>
</template>
  