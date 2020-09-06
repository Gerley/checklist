<template>
  <v-app>
    <v-app-bar app color="green" dark dense>
      <v-toolbar-title>Check-List</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-menu left bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn icon v-bind="attrs" v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item>
            <v-list-item-title @click="removerTarefasMarcadas">Remover tarefas marcadas</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>

    <v-main>
      <v-container fluid>
        <check-list
          :tarefas="tarefas"
          :tarefasMarcadas="tarefasMarcadas"
          @add-tarefa="addTarefa"
          @mark-tarefa="markTarefa"
        ></check-list>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import CheckList from "./components/CheckList";

export default {
  name: "App",

  components: { CheckList },

  data: () => ({
    tarefas: [],
    tarefasMarcadas: [],
  }),

  methods: {
    removerTarefasMarcadas() {
      this.tarefasMarcadas.sort((a, b) => b - a);

      this.tarefasMarcadas.forEach((index) => {
        this.tarefas.splice(index, 1);
      });
    },
    addTarefa(tarefa) {
      this.tarefas.push(tarefa);
    },
    markTarefa(tarefasMarcadas) {
      this.tarefasMarcadas = tarefasMarcadas;
    },
  },
};
</script>
