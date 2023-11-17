<template>
  <section class="add-todo">
    <form v-if="isFormFisible" class="add-todo__form" @submit.prevent="addTodo">
      <button class="close-button" type="button" @click="closeForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input class="input" v-model="todoText" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import { Todo } from "@/types/Todo";
import { defineComponent } from "vue";

interface State {
  isFormFisible: boolean;
  todoText: string;
}

export default defineComponent({
  data(): State {
    return {
      isFormFisible: false,
      todoText: "",
    };
  },
  methods: {
    showForm() {
      this.isFormFisible = true;
    },
    closeForm() {
      this.isFormFisible = false;
    },
    addTodo() {
      this.$emit("addTodo", {
        id: Date.now(),
        text: this.todoText,
        completed: false,
      });
    },
  },
  emits: {
    addTodo: (todo: Todo) => todo,
  },
});
</script>
