<template>
  <div class="todo">
    <h1 :class="{ checked }">
      {{ title }}
    </h1>
    <div class="button-container">
      <button
        class="button-change"
        :class="checked ? 'complete' : 'not-complete'"
        @click="checked = !checked"
      >
        {{ checked ? "Отменить выполнение" : "Выполнить" }}
      </button>
      <button @click="deleteTodo(id)" class="delete">&times;</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    id: Number,
    title: String,
    completed: Boolean,
    deleteTodo: Function,
  },
  data() {
    return {
      checked: this.completed,
    };
  },
  computed: {
    style() {
      return this.checked
        ? { "text-decoration": "line-through" }
        : { "text-decoration": "none" };
    },
  },
};
</script>

<style>
.todo {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.button-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

h1 {
  color: white;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

h1::after {
  content: " ";
  width: 0;
  height: 4px;
  background: black;
  position: absolute;
  bottom: 40%;
  border-radius: 25px;
  transition: 300ms;
}

.checked::after {
  width: 102.5%;
  border: 1px solid white;
}

.delete {
  color: darkred;
  outline: none;
  background: none;
  border: none;
  font-size: 36px;
  transition: 300ms;
}

.delete:hover {
  color: red;
}

.button-change {
  outline: none;
  border: none;
  font-size: 16px;
  border-radius: 25px;
  padding: 10px 25px;
  font-weight: bold;
  transition: 300ms;
  color: white;
}

.not-complete {
  background: rgb(0, 189, 126);
}

.not-complete:hover {
  background: rgb(0, 112, 75);
}

.complete {
  background: red;
}

.complete:hover {
  background: darkred;
}
</style>
