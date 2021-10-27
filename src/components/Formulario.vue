<template>
  <div class="box formulario">
    <div class="columns">
      <div
        class="column is-8"
        role="form"
        aria-label="Formulary to create a new task"
      >
        <input
          type="text"
          class="input"
          placeholder="What task do you want to do?"
          v-model="descricao"
        />
      </div>
      <div class="column">
        <Temporizador @aoTemporizadorFinalizado="finalizarTarefa" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import Temporizador from "./Temporizador.vue";

export default defineComponent({
  name: "Formulario",

  emits: ["aoSalvarTarefa"],

  components: {
    Temporizador,
  },

  data() {
    return {
      descricao: "",
    };
  },

  methods: {
    finalizarTarefa(tempoDecorrido: number): void {
      this.$emit("aoSalvarTarefa", {
        duracaoEmSegundos: tempoDecorrido,
        descricao: this.descricao,
      });
      this.descricao = "";
    },
  },
});
</script>

<style>
.formulario {
  background-color: var(--bg-primario);
  color: var(--texto-primario);
}
</style>
