<template>
  <div>
    <v-text-field label="Nova Tarefa" v-model="novaTarefa" @keypress="adicionarTarefa"></v-text-field>

    <v-list subheader two-line flat>
      <v-list-item-group :value="tarefasMarcadas" @change="change" multiple>
        <v-list-item v-for="tarefa in tarefas" :key="tarefa">
          <template v-slot:default="{ active }">
            <v-list-item-action>
              <v-checkbox :input-value="active" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title v-bind:class="{'text-decoration-line-through':active}">{{tarefa}}</v-list-item-title>
            </v-list-item-content>
          </template>
        </v-list-item>
      </v-list-item-group>
    </v-list>
    {{keypress}}
  </div>
</template>

<script>
export default {
  props: {
    tarefas: {
      type: Array,
      required: true,
    },
    tarefasMarcadas: {
      type: Array,
      required: true,
    },
  },
  data: () => ({
    novaTarefa: null,
    keypress: null
  }),
  methods: {
    adicionarTarefa(event) {
      this.keypress = event.code
      if (event.code == "Enter") {
        this.$emit("add-tarefa", this.novaTarefa);
        this.novaTarefa = null;
      }
    },
    change(event) {
      this.$emit("mark-tarefa", event);
    },
  },
};
</script>