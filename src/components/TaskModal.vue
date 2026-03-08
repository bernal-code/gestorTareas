<template>
  <Transition name="fade">
    <div v-if="isOpen" class="fixed inset-0 z-50 flex items-center justify-center p-4">
      <div class="fixed inset-0 bg-black/70" @click="$emit('close')"></div>

      <div class="modal-content bg-[#202020] border border-[#2F2F2F] rounded-2xl shadow-2xl w-full max-w-2xl z-10 overflow-hidden transform transition-all relative">
        
        <div class="flex items-center justify-between p-6 border-b border-[#2F2F2F]">
          <h3 class="text-xl font-semibold text-white">Editar Tarea</h3>
          
          <div class="flex items-center gap-3">
            <button 
              @click="$emit('delete', editableTask.id)"
              class="text-xs px-3 py-1.5 rounded-md bg-red-950/50 text-red-300 hover:bg-red-900 transition-colors"
            >
              Eliminar
            </button>
            
            <button @click="$emit('close')" class="text-gray-500 hover:text-white transition-colors text-2xl leading-none">
              &times;
            </button>
          </div>
        </div>

        <div class="p-6 space-y-6">
          <div>
            <div class="flex justify-between items-end mb-2">
              <label class="block text-xs uppercase tracking-wider text-gray-500 font-mono">Título</label>
              <span class="text-[10px] text-gray-600 font-mono">{{ editableTask.content?.length || 0 }}/50</span>
            </div>
            <input 
              v-model="editableTask.content" 
              type="text"
              maxlength="50" 
              class="w-full bg-[#191919] border border-[#2F2F2F] rounded-lg px-4 py-3 text-white text-lg focus:ring-2 focus:ring-blue-600 outline-none transition"
              placeholder="¿Qué hay que hacer?"
            />
          </div>

          <div>
            <div class="flex justify-between items-end mb-2">
              <label class="block text-xs uppercase tracking-wider text-gray-500 font-mono">Descripción Detallada</label>
              <span class="text-[10px] text-gray-600 font-mono">{{ editableTask.description?.length || 0 }}/200</span>
            </div>
            <textarea 
              v-model="editableTask.description" 
              maxlength="200" 
              rows="6"
              class="w-full bg-[#191919] border border-[#2F2F2F] rounded-lg px-4 py-3 text-white text-sm focus:ring-2 focus:ring-blue-600 outline-none resize-none transition no-scrollbar"
              placeholder="Añade más contexto..."
            ></textarea>
          </div>
        </div>

        <div class="p-6 bg-[#252525] border-t border-[#2F2F2F] flex justify-end gap-3">
          <button 
            @click="$emit('close')"
            class="px-5 py-2 rounded-lg text-gray-300 hover:bg-[#2F2F2F] transition-colors text-sm"
          >
            Cancelar
          </button>
          <button 
            @click="$emit('save', editableTask)"
            class="px-5 py-2 rounded-lg bg-blue-600 text-white hover:bg-blue-700 transition-colors text-sm font-semibold shadow-lg shadow-blue-900/20"
          >
            Guardar Cambios
          </button>
        </div>
      </div>
    </div>
  </Transition>
</template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  const props = defineProps(['isOpen', 'task']);
  const emit = defineEmits(['close', 'save', 'delete']);
  const editableTask = ref({});
  
  watch(() => props.task, (newTask) => {
    if (newTask) {
      editableTask.value = { ...newTask };
    }
  }, { immediate: true });
  </script>
  
<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

.fade-enter-from .modal-content, 
.fade-leave-to .modal-content {
  transform: scale(0.9) translateY(20px);
}

.modal-content {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
</style>