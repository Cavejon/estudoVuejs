<template>
  <div class="tile flex-centered" :class="{checked: tarefa.checked}">
    <div class="tile-icon">
      <i class="icon" :class="tarefa.checked ?  'icon-check' : 'icon-time'"></i>
    </div>
    <dir class="tile-content">
      <div class="tile-subtile">{{ tarefa.description }}</div>
    </dir>
    <div class="tile-action">
      <button @click="$emit('toggle', tarefa)" class="btn btn-link">
       <span v-if="tarefa.checked">Desmarcar</span> 
        <span v-else>
       Concluída</span>
      </button>
      <button @click="$emit('remove', tarefa)" class="btn btn-link">
        <span class="text-error">Remover</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tarefa: { type: Object, required: true },
  },
};
</script>

<style scoped>
 .checked{
  text-decoration: line-through;
  color: lightgray;
 }
</style>