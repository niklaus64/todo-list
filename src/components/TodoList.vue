<template>
  <div id="todolist">
    <todo
      v-on:delete-todo="deleteTodo"
      v-on:changestate-todo="changeState"
      v-for="todo in todos"
      :todo.sync="todo"
      v-bind:todo="todo"
    ></todo>
  </div>
</template>

<script type="text/javascript">
import Todo from "./Todo";

export default {
  props: ["todos"],
  components: {
    Todo
  },
  methods: {
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    changeState(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = !this.todos[todoIndex].done;
    }
  }
};
</script>
<style>
#todolist {
  margin-top: 10px;
}
</style>
