<template>
  <div class="ui basic content center aligned segment">
    <button
      class="ui basic blue button"
      v-on:click="openForm"
      v-show="!isCreating"
    >
      <i class="fork icon"></i> Dodaj zadanie
    </button>
    <div class="ui centered card" v-show="isCreating">
      <div class="content">
        <div class="ui form">
          <div class="field">
            <label>Tytuł</label>
            <input
              v-model="titleText"
              type="text"
              ref="title"
              defaultValue=""
            />
          </div>
          <div class="field">
            <label>Opis</label>
            <input
              v-model="projectText"
              type="text"
              ref="project"
              defaultValue=""
            />
          </div>
          <div class="ui two button attached buttons">
            <div class="ui labeled button" tabindex="0"></div>
            <button class="ui basic blue button" v-on:click="sendForm();">
              Stwórz
            </button>
            <button class="ui basic red button" v-on:click="closeForm">
              Anuluj
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titleText: "",
      projectText: "",
      isCreating: false
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
      if (this.titleText.length > 0 && this.projectText.length > 0) {
        const title = this.titleText;
        const project = this.projectText;
        this.$emit("create-todo", {
          title,
          project,
          done: false
        });
        this.titleText = "";
        this.projectText = "";
      }
      this.isCreating = false;
    }
  }
};
</script>
