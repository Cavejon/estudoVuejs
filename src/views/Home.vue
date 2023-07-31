<template>
     <div class="container grid-xs py-2">
      <img
        class="img-responsive img-logo"
        src="@/assets/avatar.png"
        alt="avatar"
      />
      <form @submit.prevent="addTarefas(tarefa)">
        <div class="input-group">
          <input
            type="text"
            v-model="tarefa.description"
            class="form-input"
            placeholder="Escreva a tarefa"
          />
          <button class="btn btn-primary input-group-btn">Adicionar</button>
        </div>
      </form>
      <div class="tarefa-list">
        <tarefa
          v-for="t in tarefas"
          :key="t.id"
          @toggle="toggleTarefa"
          @remove="removeTarefa"
          :tarefa="t"
        />
      </div>
    </div>
</template>


<script>
import Tarefa from "@/components/Tarefa-component";

export default {
  name: "App",
  components: { Tarefa },
  data() {
    return { tarefas: [], tarefa: { checked: false } };
  },
  methods: {
    addTarefas(tarefa) {
      tarefa.id = Date.now();
      this.tarefas.push(tarefa);
      this.tarefa = { checked: false };
    },
    toggleTarefa(tarefa) {
      const index = this.tarefas.findIndex((item) => item.id === tarefa.id);
      if (index > -1) {
        const checked = !this.tarefas[index].checked;
        this.$set(this.tarefas, index, { ...this.tarefas[index], checked });
      }
    },
    removeTarefa(tarefa) {
      const index = this.tarefas.findIndex((item) => item.id === tarefa.id);
      if (index > -1) {
        this.$delete(this.tarefas, index);
      }
    },
  },
};
</script>

<style scoped>
.img-logo {
  max-width: 300px;
  margin: 5rem auto;
  border-radius: 20px;
}

.tarefa-list {
  padding-top: 2rem;
}
</style>
