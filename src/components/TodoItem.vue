<script setup>
import { Icon } from "@iconify/vue"; // define props，props are properties passed from a parent component to a child component

// define props pass to TodoItem component
const props = defineProps({
  // ‘todo’ is the name of the prop being defined use'{}' to object
  todo: {
    //specifies type of the todo prop is object
    type: Object,
    //specifies that the todo prop is required
    required: true,
  },
  index: {
    //specifies type of the index prop is number
    type: Number,
    //specifies that the index prop is required
    required: true,
  },
});

// define emits, emits are events emitted from a child component to a parent component
defineEmits([
  "toggle-todo",
  "edit-todo-status",
  "edit-todo",
  "delete-todo",
  "toggle-important",
]);
</script>

<template>
  <li>
    <!-- check box dynamically set check box status by isCompleted, emit index of the todo item when status of todo is changed -->
    <input
      type="checkbox"
      :checked="todo.isCompleted"
      @input="$emit('toggle-todo', index)"
    />

    <!-- show todo item -->
    <div class="todo-item">
      <!-- if todo is editing, display input field -->
      <input
        v-if="todo.isEditing"
        type="text"
        :value="todo.todo"
        @input="$emit('edit-todo', $event.target.value, index)"
      />

      <!-- output value of todo prop, when todo is completed, attach class to style -->
      <span v-else :class="{ 'completed-todo': todo.isCompleted }">
        {{ todo.todo }}
      </span>
    </div>

    <!-- icon and action buttons -->
    <div class="todo-action">
      <!-- tick icon show when todo is editing -->
      <Icon
        v-if="todo.isEditing"
        icon="typcn:tick"
        width="30"
        height="30"
        style="color: #c9e4de"
        class="icon"
        @click="$emit('edit-todo-status', index)"
      />

      <!-- edit icon shown when todo is not editing -->
      <Icon
        v-else
        icon="flowbite:edit-outline"
        width="30"
        height="30"
        style="color: #dedaf4"
        class="icon"
        @click="$emit('edit-todo-status', index)"
      />

      <!-- delete icon -->
      <Icon
        icon="material-symbols-light:delete"
        width="30"
        height="30"
        style="color: #ffadad"
        class="icon"
        @click="$emit('delete-todo', todo.id)"
      />
    </div>
    <!-- important button -->
    <Icon
      :icon="todo.isImportant ? 'mage:star-fill' : 'mage:star'"
      width="30"
      height="30"
      :style="{ color: todo.isImportant ? '#ffdfba' : '#ccc6cf' }"
      class="icon-important"
      @click="$emit('toggle-important', index)"
    />
  </li>
</template>

<style lang="scss" scoped>
li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 16px 10px;
  background-color: #f1f1f1;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);
  border-radius: 4px;

  &:hover {
    .todo-action {
      opacity: 1;
    }
  }

  input[type="checkbox"] {
    appearance: none;
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50%;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);

    &:checked {
      background-color: #8fddcc;
    }
  }

  .todo-item {
    flex: 1;

    input[type="text"] {
      width: 100%;
      padding: 2px 6px;
      border: 2px solid #d6bde0;
      border-radius: 4px;
    }
  }

  .todo-action {
    display: flex;
    gap: 6px;
    opacity: 0;
    transition: 150ms ease-in-out;

    .icon {
      cursor: pointer;
    }
  }

  .completed-todo {
    text-decoration: line-through;
  }

  .icon-important {
    cursor: pointer;
    opacity: 1;
  }
}
</style>
