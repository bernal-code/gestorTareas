<template>
  <div class="task-enter group relative bg-[#262626] border border-[#2F2F2F] rounded-xl p-4 
              hover:border-blue-500/50 hover:bg-[#2a2a2a] transition-all duration-200 
              cursor-pointer hover:shadow-[0_0_20px_rgba(59,130,246,0.1)] active:scale-95">
    
    <button 
      @click.stop="$emit('quick-delete', task.id)"
      class="absolute top-1 right-1 w-5 h-5 bg-red-500 text-white rounded-full flex items-center justify-center 
             opacity-0 group-hover:opacity-100 transition-all shadow-lg hover:bg-red-600 z-20 text-[10px] font-bold"
    >
      ✕
    </button>

    <div class="flex items-start justify-between">
      <p class="text-sm font-medium text-white/90 leading-relaxed warp-break-words line-clamp-2 pr-2">
        {{ task.content || 'Sin título' }}
      </p>
    </div>
    
    <div v-if="task.description" class="mt-3 flex items-center gap-2">
      <div class="h-1 w-8 bg-blue-500/30 rounded-full"></div>
      <span class="text-[10px] text-gray-500 truncate w-full italic">
        {{ task.description }}
      </span>
    </div>
  </div>
</template>

<script setup>
defineProps(['task']);
defineEmits(['quick-delete']);
</script>