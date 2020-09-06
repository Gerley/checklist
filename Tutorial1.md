# Vuejs - PWA

O objetivo deste tutorial é criar um PWA checklist.

## 1. Criar um checklist em Vuetify

Nesta primeira parte, iremos criar um projeto Vuetify e construir as funcionalidades do checklist.

### 1.1 Criando o Projeto Vuetify
Crie um novo projeto Vue e adicione o  vuetify conforme comandos abaixo.

```sh
vue create checklist
cd checklist
vue add vuetify
```

### 1.2 Construindo o skeleton da aplicação

No arquivo App.vue, apague todos o codigo e insira o codigo abaixo.

```js
<template>
  <v-app>
    <v-app-bar app>
    </v-app-bar>

    <v-main>
      <v-container fluid>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    //
  }),
};
</script>
```

Remova o arquivo **components/HelloWorld.vue**.

### 1.3 Configurando o app-bar

No arquivo **App.vue** edite a tag v-app-bar conforme codigo abaixo:

```html
<v-app-bar app color="green" dark dense>
    <v-toolbar-title>Check-List</v-toolbar-title>
</v-app-bar>
```

### 1.4 Criando o component checklist

Crie o arquivo "CheckList.vue", e adicione o codigo abaixo:

```html
<template>
  <div>
    <v-text-field
      label="Nova Tarefa"
      v-model="novaTarefa"
      @keypress="keypressNovaTarefa"
      append-outer-icon="mdi-send"
      @click:append-outer="adicionarTarefa"
    ></v-text-field>

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
    keypress: null,
  }),
  methods: {
    keypressNovaTarefa(event) {
      this.keypress = event.code;
      if (event.code == "Enter") {
        this.adicionarTarefa();
      }
    },
    adicionarTarefa() {
      if (this.novaTarefa) {
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
```

### 1.5 Adicionando o componente CheckList ao App

No arquivo App, atualize a tag v-app-bar, conforme codigo abaixo:

```html
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
    ...
```

Dentro de v-container, adicione o codigo abaixo.
```html
<v-container fluid>
        <check-list
          :tarefas="tarefas"
          :tarefasMarcadas="tarefasMarcadas"
          @add-tarefa="addTarefa"
          @mark-tarefa="markTarefa"
        ></check-list>
      </v-container>
```

Por ultimo, adicione o script abaixo:
```js
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
```



