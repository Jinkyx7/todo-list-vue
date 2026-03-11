# Todo List Vue

A small todo list application built with Vue 3 and Vite. The app supports creating, editing, completing, deleting, and prioritizing todos, with state persisted in `localStorage`.

## Features

- Add and edit todos inline
- Mark todos as completed
- Mark important todos and sort them to the top
- Clear completed items or reset the whole list
- Persist todos in the browser with `localStorage`

## Screenshoot

![Todo List Vue.js](./src/assets/Todo%20List%20Demo%20Screenshot.png)

## Tech Stack

- Vue 3
- Vue Router
- Vite
- Sass
- Iconify

## Project Structure

```text
project-root/
│
├── public/                  # Public assets
│
├── src/                     # Source code
│   ├── App.vue              # Root Vue component
│   ├── main.js              # Entry point, Vue app initialization
│   │
│   ├── assets/              # Static assets (images, fonts, etc.)
│   │   ├── logo.png         # Logo image
│   │   └── screenshoot.png  # Screenshot image
│   │
│   ├── components/          # Vue components
│   │   ├── TodoButton.vue   # Component for generic button
│   │   ├── TodoCreator.vue  # Component for creating new todo items
│   │   ├── TodoHeader.vue   # Component for header and navigation
│   │   └── TodoItem.vue     # Component for displaying individual todo items
│   │
│   ├── router/              # Vue Router configuration
│   │   └── index.js         # Router configuration file
│   │
│   ├── views/               # Vue views/pages
│       ├── AboutView.vue    # About page view
│       ├── NotFoundView.vue # 404 Not Found page view
│       └── TodoView.vue     # Main todo list view
│
│── index.html               # Main HTML template
├── README.md                # Project README file
├── package.json             # Project dependencies and scripts
└── ...

```

## Getting Started

### Prerequisites

- Node.js 18+ recommended

### Install

```sh
npm install
```

### Run the app

```sh
npm run dev
```

The Vite dev server will print the local URL, typically `http://localhost:5173/`.

## Available Scripts

- `npm run dev`: start the development server
- `npm run build`: create a production build in `dist/`
- `npm run preview`: preview the production build locally

# Important Concepts and Elements

### Component Structure/Hierarchy

```sh
App.vue
└── TodoHeader.vue
└── RouterView
    ├── AboutView.vue
    ├── NotFoundView.vue
    └── TodosView.vue
        ├── TodoCreator.vue
        │   └── TodoButton.vue
        ├── TodoItem.vue
        └── TodoButton.vue
```

## Core Vue Fundamentals

### Initialise Vue Application

The code sets up a Vue application by creating a Vue application instance with `createApp`, integrating Vue Router using `app.use`, and then mounting the Vue application onto a specific DOM element with `app.mount`. This structure is typical for setting up a Vue application with routing capabilities

```sh
# Main.js
const app = createApp(App);

app.use(router);

app.mount("#app");
```

### Route Configurations

Vue Router is used for client-side routing, enabling single-page applications with multiple views/pages without requiring full page refreshes. Initialises a Vue Router instance using the `createRouter` function and configures routes within the `routes` array. Each route configuration includes a path, name, and component to render when the path is matched. In this setup, the `TodosView` component is assigned to the root path ("/"), serving as the main entry point for the application's interface.

```sh
# index.js
const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    // Route configurations go here
     {
    path: "/",
    name: "home",
    component: TodosView,
  }
  ]
});
```

### Component Composition

Components are composed together to build the UI and functionality of the application. This modular approach allows for easier management of state within smaller, more focused components.

For example, the `TodoButton.vue` is a reusable component that has its own template and style. It uses the `<slot>` element to receive content from its parent components, namely `TodoCreator.vue` and `TodoItem.vue`. This content is then rendered within its own template via `<TodoButton />`. This approach promotes code consistency and efficiency.
**Define button in `ToodoButton.vue`**

```sh
# ToodoButton.vue
<template>
  <button>
    <slot>this is a button</slot>
  </button>
</template>
```

**Render button in `TodoCreator.vue`**

```sh
# TodoCreator.vue
    import TodoButton from "./TodoButton.vue";

    <TodoButton @click="createTodo">Add</TodoButton>

```

### Reactivity System and Vue Composition API for Component Logic

Vue's reactivity system enables the application to automatically update the UI when the underlying data changes. This is achieved through the use of reactive data properties and computed properties

The Vue Composition API for Component Logic is a feature introduced in Vue 3 that provides a more flexible and organized way to manage component logic compared to the Options API. It allows developers to compose logic using functions, making it easier to reuse and organise code.

In the project, all the Composition API functions are reactive. Here are some examples:

**Reactive State with `ref`**

`ref` is used to create reactive state variables within a component.

```sh
# TodoView.vue
import { ref } from "vue";

const todoList = ref([]);
```

In the project, `ref` is used to create reactive references for the todo list, this means that any changes made to todoList will trigger reactivity updates in the UI.

**Reactive Computations with `computed`**

`computed` is used to create reactive computed properties based on other reactive properties.

```sh
# TodoView.vue
import { computed } from "vue";

const completedTodo = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});
```

In the project, `computed` is used to derive the `completedTodo` property based on the completion status of todos in the todo list. It automatically updates whenever todoList changes.

**Reactive Effects with `watch`**

`watch` is used to perform side effects in response to changes in reactive properties.

```sh
# TodoView.vue
import { watch } from "vue";

watch(
  todoList,
  () => {
    setTodoListLocalStorage();
  },
  { deep: true }
);
```

In the project, `watch` is employed to watch changes in the todo list and calls setTodoListLocalStorage() when it detects a change.

**Reactive Refs with `reactive`**

`reactive` is used to create reactive objects or nested data structures.

```sh
# TodoCreator.vue
import { reactive } from "vue";

const todoState = reactive({
  todo: "",
  isValid: true,
  errorMessage: "",
});
```

In the project, `reactive` is used to create a reactive object `todoState`, any changes to its properties (todo, isValid, errorMessage) will be automatically tracked and trigger reactivity updates.

### State Management and Event Handling

State management refers to the way data is managed and shared among various components of an application.

Event handling pertains to the management of user interactions within an application. These interactions, which can alter the application's data state, may involve adding new todo items, toggling their completion status, editing or deleting them, and marking items as important.

In the project State management is handled within `TodoView.vue` using Vue's reactivity system (ref).

**Reactive Variables**

This code establishes a reactive reference, `todoList`, to hold a list of todo items. It also provides a function, `createTodo`, to add new todo objects to the list. Each Todo object has properties like `id`, `todo`, `isCompleted`, `isEditing`, and `isImportant`. These properties signify different states and attributes of a todo item. By using `ref`, any modifications to `todoList` will automatically prompt reactivity updates in Vue components that reference it.

```sh
# TodoView
import { ref } from 'vue';

const todoList = ref([]);

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: false,
    isEditing: false,
    isImportant: false,
  });
};
```

let’s take an example of **toggle completion**, and see how the event changes state

**Props**

Components can receive data from their parent components via props. This allows parent components to pass down data to child components, enabling communication and sharing of state.

Child component:

```sh
# TodoItem.vue
 import { defineComponent } from 'vue';

 const props = defineProps({

  todo: {
    type: Object,
    required: true,
  },
```

`TodoItem.vue` is a child component that receives a `todo` object as a prop from its parent component.

The `props` option inside the component definition object is used to define the props that the component expects to receive.

In this case,`todo` is defined as a prop, specifying that it should be an object (`type: Object`) and is required (`required: true`). This means that the parent component must pass a `todo` object to `TodoItem` for it to function properly.

Parent component:

```sh
# TodosView.vue
<TodoItem
   v-for="(todo, index) in todoList"
   :todo="todo"
   :index="index"
/>
```

parent component `TodosView` iterates over a list of todo items and renders a child component (`<TodoItem>`) for each item. It passes down the todo item(`:todo="todo"`) and its index (`:index="index"`) as props to the `<TodoItem>` component, allowing the child component to access and display the data.

**Emit Event**

Child components can emit custom events to notify their parent components about changes or actions. This allows for communication from child to parent, enabling parent components to react to changes in state.

Child Component:

```sh
# TodoItem.vue
defineEmits([
  "toggle-todo",
]);

<input
  type="checkbox"
  :checked="todo.isCompleted"
  @input="$emit('toggle-todo', index)" <!-- Emits 'toggle-todo' event with the index -->
/>
```

**`defineEmits(['toggle-todo'])`** declares that the child component emits a custom event named 'toggle-todo'. This step is important for Vue to recognise that this component can emit such an event.
**`@input="$emit('toggle-todo', index)`** listens for the 'input' event and emits a custom event 'toggle-todo' with the 'index' of the todo item as the payload.

When the checkbox is clicked, the 'toggle-todo' event is emitted to the parent component with the index of the corresponding todo item.

Parent component:

```sh
# TodosView.vue
<TodoItem
const toggleTodo = (index) => {
  todoList.value[index].isCompleted = !todoList.value[index].isCompleted;
};

  v-for="(todo, index) in todoList"
  :todo="todo"
  :index="index"
  @toggle-todo="toggleTodo"
/>
```

**`@toggle-todo="toggleTodo"`** listens for the 'toggle-todo' event emitted by the child component (TodoItem) and calls the 'toggleTodo' function when the event is triggered

**`toggleTodo`** function receives the 'index' of the todo item, which is emitted from the child component as a parameter. It toggles the completion status of the todo item at the given index by negating its current value.

### LocalStorage for Data Persistence

`LocalStorage` is used for storing the todo list locally in the browser

```sh
# TodosView.vue
const fetchTodoListLocalStorage = () => {
  const todoListData = JSON.parse(localStorage.getItem("todoList"));
  if (todoListData) {
    todoList.value = todoListData;
  }
};

const setTodoListLocalStorage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};
```

**`fetchTodoListLocalStorage`** is a function responsible for fetching the todo list data from Local Storage.

**`setTodoListLocalStorage`** is a function responsible for setting the todo list data in Local Storage.

Local Storage in web browsers enables persistent data storage. This feature allows applications to preserve user data, such as a todo list, even after the user closes the browser, navigates away from the page, or refreshes the page. It enhances the user experience by preventing data loss.

## Reference

[1] Creating a Vue Application - https://vuejs.org/guide/essentials/application.html

[2] Reactivity Fundamentals - https://vuejs.org/guide/essentials/reactivity-fundamentals

[3] Conditional Rendering - https://vuejs.org/guide/essentials/conditional.html

[4] Event Handling - https://vuejs.org/guide/essentials/event-handling.html

[5] Props - https://vuejs.org/guide/components/props.html

[6] Component Events - https://vuejs.org/guide/components/events.html

[7] Routing - https://vuejs.org/guide/scaling-up/routing.html

[8] State Management - https://vuejs.org/guide/scaling-up/state-management.html
