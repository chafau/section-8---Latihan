<template>
  <div class="container">
    <h2>{{ listName }}</h2>
    <hr v-if="this.todos.length > 0"/>
    <div class="row">
      <div>
        <ol>
          <todo
            v-for="(todo, index) in todos"
            :key="index"
            :description="todo.description"
            @on-toggle="toggleTodo(todo)"
            @on-delete="deleteTodo(todo)"
            @on-edit="editTodo(todo, $event)"
          />
        </ol>
      </div>
    </div>
    <div class="row">
      <div><hr v-if="this.todos.length > 0" /></div>
    </div>
    <div class="row">
      <create-todo @on-new-todo="addTodo($event)" />
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";
import CreateTodo from "./CreateTodo.vue";

export default {
  props: {
    listName: String,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push({ description: newTodo, completed: false });
      console.log(newTodo);
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    deleteTodo(deletedTodo) {
      this.todos = this.todos.filter((todo) => todo !== deletedTodo);
    },
    editTodo(todo, newTodoDescription) {
      todo.description = newTodoDescription;
    },
  },
  components: { Todo, CreateTodo },
};
</script>

<style>
h2 {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: block;
  font-size: 1.5em;
  margin-block-start: 0.83em;
  margin-block-end: 0.83em;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
  font-weight: bold;
  text-align: center;
}

hr {
  margin-top: 20px;
  margin-bottom: 20px;
}
</style>