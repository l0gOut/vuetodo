<template>
  <div class="todo-container">
    <h1 v-if="warning">{{ warning }}</h1>
    <div class="input-container">
      <input
        @keydown="changeInput"
        @keyup.enter="addTodo"
        v-model="inputText"
        type="text"
      />
      <button @click="addTodo">Добавить</button>
    </div>
    <hr />
    <div v-if="todos.length" class="todos-container">
      <Todo
        v-for="todo in todos"
        :id="todo.id"
        :title="todo.title"
        :completed="todo.completed"
        :deleteTodo="deleteTodo"
        :key="todo.id"
      />
    </div>
    <div class="todos-clear" v-else><h1>Задач нет!</h1></div>
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";

export default {
  name: "App",
  components: {
    Todo,
  },
  data() {
    return {
      warning: "",
      inputText: "",
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (this.inputText.length === 0)
        this.warning = "Поле должно быть заполнено!";
      else {
        this.warning = "";
        let idTodo = 1;
        for (let i of this.todos) {
          if (i.id === idTodo) continue;
        }
        this.todos.push({
          id: idTodo,
          title: this.inputText,
          completed: false,
        });
        this.inputText = "";
      }
    },
    deleteTodo(n) {
      this.todos.splice(n - 1, 1);
      console.log(this.todos);
    },
    changeInput() {
      this.warning = false;
    },
  },
};
</script>

<style>
.todo-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}

.todos-container {
  width: 50%;
}

.todos-clear {
  color: white;
  font-weight: bold;
  font-size: 36px;
}

.todos-clear > h1 {
  padding: 0;
  margin: 0;
}

.input-container {
  width: 50%;
  display: flex;
  justify-content: space-around;
}

.input-container > input {
  outline: none;
  border-width: 0 0 1px 0;
  border-color: white;
  color: white;
  background: none;
  font-size: 24px;
}
.input-container > button {
  outline: none;
  border: none;
  background: rgb(0, 109, 109);
  color: white;
  border-radius: 25px;
  font-size: 16px;
  font-weight: bold;
  padding: 10px 25px;
  transition: 300ms;
}

.input-container > button:hover {
  background: rgb(0, 180, 180);
}

hr {
  width: 50%;
}
</style>
