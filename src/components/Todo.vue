<template>
  <div class="ui centered card">
    <div class="content" v-show="!isEditing">
      <div class="header">{{ todo.title }}</div>
      <div class="meta">{{ todo.project }}</div>
      <div class="extra content">
        <span class="right floated edit icon" v-on:click="showForm">
          <i class="edit icon"></i>
        </span>
        <span class="right floated trash icon" v-on:click="deleteTodo(todo);">
          <i class="trash icon"></i>
        </span>
      </div>
    </div>
    <div class="content" v-show="isEditing">
      <div class="ui form">
        <div class="field">
          <label>Tytuł</label> <input type="text" v-model="todo.title" />
        </div>
        <div class="field">
          <label>Opis</label> <input type="text" v-model="todo.project" />
        </div>
        <div class="ui two button attached buttons">
          <button class="ui basic blue button" v-on:click="hideForm">
            Zatwierdź
          </button>
        </div>
      </div>
    </div>
    <div
      class="ui bottom attached green basic button"
      v-show="!isEditing && todo.done"
      v-on:click="changeState(todo);"
    >
      Zakończone
    </div>
    <div
      class="ui bottom attached red basic button"
      v-show="!isEditing && !todo.done"
      v-on:click="changeState(todo);"
    >
      W trakcie
    </div>
  </div>
</template>

<script>
export default {
  props: ["todo"],
  data() {
    return {
      isEditing: false,
      done: false
    };
  },
  methods: {
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
    deleteTodo(todo) {
      this.$emit("delete-todo", todo);
    },
    changeState(todo) {
      this.$emit("changestate-todo", todo);
    }
  }
};
</script>
