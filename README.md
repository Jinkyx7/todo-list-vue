# Todo List Vue

A small todo list application built with Vue 3 and Vite. The app supports creating, editing, completing, deleting, and prioritizing todos, with state persisted in `localStorage`.

## Features

- Add and edit todos inline
- Mark todos as completed
- Mark important todos and sort them to the top
- Clear completed items or reset the whole list
- Persist todos in the browser with `localStorage`

## Tech Stack

- Vue 3
- Vue Router
- Vite
- Sass
- Iconify

## Project Structure

```text
.
├── public/
├── src/
│   ├── assets/
│   ├── components/
│   ├── router/
│   ├── views/
│   ├── App.vue
│   └── main.js
├── index.html
├── package.json
└── vite.config.js
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
