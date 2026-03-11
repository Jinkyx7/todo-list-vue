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

## Routes

- `/`: main todo list
- `/about`: short app description
- `/*`: not found page

## Notes

- Todo data is stored locally in the browser and is not shared across devices.
- There is currently no automated test suite configured for this project.
