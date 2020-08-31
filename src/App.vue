<template>
  <div id="app">
    <div class="insert">
      <h3>{{title}}</h3>
      <form>
        <input type="text" id="newTodo" v-model="newTodo" v-on:submit.prevent="addTodo" />
        <button v-on:click.prevent="addTodo" id="addTodo">Adicionar</button>
      </form>
      <button @click="allDone" class="allDone">Concluir Tarefas</button>
    </div>
    <div class="lista">
      <ul v-for="todo in todos" :key="todo.title">
        <li>
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ done: todo.done }">{{todo.title}}</span>
          <button @click="removeTodo(todo)">Remover</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      title: "Lista de Tarefas",
      newTodo: "",
      todos: [],
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        done: false,
      });
      this.newTodo = "";
    },
    removeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    allDone() {
      this.todos.forEach((todo) => {
        todo.done = true;
      });
    },
  },
};
</script>

<style>
#app {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.done {
  text-decoration: line-through;
}

.insert {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
#newTodo {
  width: 200px;
}
#addTodo {
  width: 100px;
}
.allDone {
  width: 310px;
}
.lista {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 300px;
  margin: 15px auto;
}
.lista ul {
  padding-inline-start: 0px;
  margin: 5px;
}
.lista ul li {
  display: flex;
  justify-content: space-evenly;
  list-style: none;
  margin: 5 auto;
  min-width: 300px;
}
</style>
