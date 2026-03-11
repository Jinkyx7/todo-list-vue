<script setup>
import { defineEmits, reactive } from "vue";
import TodoButton from "./TodoButton.vue";

// to make an emit from the child component to the parent component
const emit = defineEmits(["create-todo"]);

const todoState = reactive({
  todo: "",
  isValid: true,
  errorMessage: "",
});

//emit event 'create-todo' and the todo value to the parent component
const createTodo = () => {
  // check if the todo is valid
  if (todoState.todo !== "" && todoState.todo.length > 2) {
    emit("create-todo", todoState.todo);
    todoState.isValid = true;
    todoState.errorMessage = "";
    todoState.todo = "";
  } else {
    todoState.isValid = false;
    todoState.errorMessage = "Please enter a valid todo";
  }
};
</script>

<template>
  <!-- dynamic class -->
  <div class="input-text" :class="{ 'input-error': !todoState.isValid }">
    <!-- any changes made to the input field will update(synced) the todo reference -->
    <input type="text" placeholder="Add a new todo" v-model="todoState.todo" />

    <!-- emit event to the parent component -->
    <TodoButton @click="createTodo">Add</TodoButton>
  </div>

  <!-- show error message if the todo is not valid -->
  <p v-show="!todoState.isValid" class="err-msg">
    {{ todoState.errorMessage }}
  </p>
</template>

<style lang="scss" scoped>
.input-text {
  display: flex;
  transition: 250ms ease;
  border: 2.5px solid #d6bde0;
  border-radius: 4px;

  &.input-error {
    border-color: rgb(236, 86, 86);
  }

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }
}

.err-msg {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: rgb(236, 86, 86);
}
</style>
