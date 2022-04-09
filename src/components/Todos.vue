<template>
  <div class="todos">
    <div v-for="(todo, index) in todos" :key="index">
      <Todo
        :description="todo.description"
        :isCompleted="todo.isCompleted"
        :index="index"
        @toggleCompleted="toggleCompleted"
        @remove="remove"
      />
    </div>

    <div class="todo my-3 d-flex justify-content-between">
      <input
        class="my-2 mx-2"
        v-model="newTodo"
        type="text"
        placeholder="New todo..."
        @keyup.enter="add"
      />
      <i class="material-icons icons mt-2 px-2" @click="add">add</i>
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  name: "Todos",

  data() {
    return {
      newTodo: "",
      todos: [],
    };
  },

  mounted() {
    // TODO: Use Firestore + Google Auth
    const savedTodos = localStorage.getItem("todos");
    if (savedTodos) this.todos = JSON.parse(savedTodos);
  },

  methods: {
    save() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },

    add() {
      if (this.newTodo === "") return;
      this.todos.push({ description: this.newTodo, isCompleted: false });
      this.newTodo = "";
      this.save();
    },

    remove(index) {
      this.todos.splice(index, 1);
      this.save();
    },

    toggleCompleted(index) {
      this.todos[index].isCompleted = !this.todos[index].isCompleted;
      this.save();
    },
  },

  components: {
    Todo,
  },
};
</script>

<style>
.todos {
  max-width: 75%;
  margin: auto;
}

.todo {
  border: 2px solid rgb(129, 129, 129);
  border-radius: 5px;
}

i {
  color: rgb(90, 90, 90);
  cursor: pointer;
}

input {
  width: 95%;
  outline: none;
  border: 0;
  border-bottom: 1px solid rgba(90, 90, 90, 0);
  transition: 0.25s;
}

input:focus {
  border-bottom: 1px solid rgb(90, 90, 90);
  transition: 0.25s;
}
</style>