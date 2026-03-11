<script setup>
import { ref, watch, computed } from "vue";
import { uid } from "uid";
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";
import TodoButton from "../components/TodoButton.vue";

// create reactive references for todo list
const todoList = ref([]);

// watch changes in todoList and save to local storage
watch(
  todoList,
  () => {
    setTodoListLocalStorage();
  },
  { deep: true }
);

// fetch todo list from local storage
const fetchTodoListLocalStorage = () => {
  const todoListData = JSON.parse(localStorage.getItem("todoList"));
  if (todoListData) {
    todoList.value = todoListData;
  }
};

// Sort todo list based on importance
const sortTodoList = () => {
  const importantTodos = todoList.value.filter((todo) => todo.isImportant);
  const nonImportantTodos = todoList.value.filter((todo) => !todo.isImportant);
  todoList.value = [...importantTodos, ...nonImportantTodos];
};

// each time page is loaded, fetch todo list from local storage
fetchTodoListLocalStorage();

// save todo list to local storage
const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: false,
    isEditing: false,
    isImportant: false,
  });
};

// automatically checks reactive dependencies(every time when todolist value updates) and updates the computed value (true or false)
const completedTodo = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});

// receive index of the todo item and update todo status
const toggleTodo = (index) => {
  todoList.value[index].isCompleted = !todoList.value[index].isCompleted;
};
const editTodoStatus = (index) => {
  todoList.value[index].isEditing = !todoList.value[index].isEditing;
};
const editTodo = (todo, index) => {
  todoList.value[index].todo = todo;
};
const deleteTodo = (id) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== id);
};

const toggleImportant = (index) => {
  todoList.value[index].isImportant = !todoList.value[index].isImportant;
  sortTodoList();
};
const clearCompletedTodo = () => {
  todoList.value = todoList.value.filter((todo) => !todo.isCompleted);
};
const clearAllTodo = () => {
  todoList.value = [];
};
</script>

<template>
  <main>
    <h1>✔️ Todo List</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul class="todo-list" v-if="todoList.length > 0">
      <!-- render each todo item, pass todo and index param as prop to TodoItem component  -->
      <TodoItem
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        @toggle-todo="toggleTodo"
        @edit-todo-status="editTodoStatus"
        @edit-todo="editTodo"
        @delete-todo="deleteTodo"
        @toggle-important="toggleImportant"
      />
      <div class="button-container">
        <TodoButton @click="clearCompletedTodo" class="clear-button"
          >Clear Completed</TodoButton
        >
        <TodoButton @click="clearAllTodo" class="clear-button"
          >Clear All</TodoButton
        >
      </div>
    </ul>
    <p v-else class="message">
      <span>🤓 You don't have anything in your list! 👆🏼Add one! </span>
    </p>
    <p v-if="completedTodo && todoList.length > 0" class="message">
      <span>🎉 Congrats! You have completed all your todos! 🎉</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 600px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;
  color: rgb(51, 49, 49);

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .button-container {
    display: flex;
    gap: 10px;
  }

  .clear-button {
    flex: 1;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .message {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
    font-size: 15px;
  }
}
</style>
