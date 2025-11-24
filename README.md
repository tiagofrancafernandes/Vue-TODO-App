# Todo App

A modern and elegant task management application built with Vue 3, Vite, and TailwindCSS v4. This application allows you to create, manage, and track your daily tasks efficiently with automatic data persistence using the browser's LocalStorage.

<a href="https://vercel.com/new/clone?repository-url=https://github.com/tiagofrancafernandes/Vue-TODO-App/tree/master"><img src="https://vercel.com/button"></a>


## Table of Contents
- [Features](#features)
- [Technologies](#technologies)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Data Persistence](#data-persistence)
- [Available Scripts](#available-scripts)
- [TailwindCSS v4 Configuration](#tailwindcss-v4-configuration)
- [Browser Support](#browser-support)
- [Development](#development)
- [License](#license)
- [Contributing](#contributing)
- [Support](#support)
- [Thanks](#thanks)


## Features

✨ **Create Tasks** - Add new tasks with a simple and intuitive interface
✅ **Mark as Complete** - Toggle task completion status with a single click
🗑️ **Delete Tasks** - Remove individual tasks from your list
🔍 **Filter Tasks** - View all tasks, pending tasks, or completed tasks
📊 **Statistics Dashboard** - Real-time statistics showing total, completed, and pending tasks
💾 **LocalStorage Persistence** - All your tasks are automatically saved to your browser's LocalStorage
⌨️ **Keyboard Support** - Press Enter to quickly add a new task
🎨 **Responsive Design** - Beautiful, responsive UI that works on all devices
🌈 **Modern Styling** - Built with TailwindCSS v4 for a clean and modern look

## Technologies

- **Vue 3** - Progressive JavaScript framework with Composition API
- **Vite** - Next-generation frontend build tool
- **TailwindCSS v4** - Utility-first CSS framework with CSS-first configuration
- **LocalStorage API** - Browser's built-in data persistence
- **JavaScript ES6+** - Modern JavaScript features

## Project Structure

```
.
├── src/
│   ├── App.vue           # Main application component with all logic
│   ├── main.js           # Application entry point
│   ├── style.css         # Global styles with TailwindCSS import
│   └── assets/           # Static assets (images, etc.)
├── vite.config.js        # Vite configuration with TailwindCSS plugin
├── index.html            # HTML entry point
└── package.json          # Project dependencies
```

## Installation

### Prerequisites

- **Node.js** (v16 or higher)
- **npm** (v7 or higher) or **yarn**

### Setup Steps

1. **Clone or navigate to the project directory:**
   ```bash
   cd app-directory
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Start the development server:**
   ```bash
   npm run dev
   ```

4. **Open in your browser:**
   The application will be available at `http://localhost:5174/`

## Usage

### Adding a Task
1. Type your task in the input field
2. Press **Enter** or click the **Add** button
3. Your task will appear in the list and be saved automatically

### Completing a Task
- Click the checkbox next to a task to mark it as complete
- Completed tasks will be displayed with a strikethrough

### Deleting a Task
- Click the **Delete** button on any task to remove it from your list

### Filtering Tasks
- Use the filter buttons to view:
  - **All** - All tasks (default)
  - **Pending** - Only incomplete tasks
  - **Completed** - Only completed tasks

### Clearing Completed Tasks
- When you have completed tasks, a **Clear Completed Tasks** button appears
- Click it to remove all completed tasks at once

## Data Persistence

This application uses the browser's **LocalStorage API** to persist your tasks. Your data is stored locally on your device and will be available when you:
- Refresh the page
- Close and reopen the browser
- Return to the application later

**Note:** LocalStorage is browser-specific. Tasks saved in Chrome won't appear in Firefox or Safari.

## Available Scripts

### Development Server
```bash
npm run dev
```
Starts the Vite development server with hot module reloading (HMR)

### Build for Production
```bash
npm run build
```
Creates an optimized production build in the `dist/` directory

### Preview Production Build
```bash
npm run preview
```
Previews the production build locally

## TailwindCSS v4 Configuration

This project uses TailwindCSS v4 with Vite, which means:
- ✅ **No config files needed** - Configuration is CSS-first
- ✅ **Single import** - Just `@import "tailwindcss"` in your CSS
- ✅ **Automatic processing** - The Vite plugin handles all CSS generation
- ✅ **Smaller bundle** - Only includes styles you actually use

## Browser Support

This application works on all modern browsers that support:
- ES6+ JavaScript
- LocalStorage API
- CSS Grid and Flexbox

Supported browsers:
- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Opera (latest)

## Development

### Code Style

This project follows Vue 3 and JavaScript best practices:
- **Composition API** for component logic
- **Reactive references** using `ref()` and `computed()`
- **Lifecycle hooks** like `onMounted()`
- **Component scoped styles** with `<style scoped>`

### Future Enhancements

Possible improvements for future versions:
- Cloud synchronization (Firebase, Supabase)
- User authentication and accounts
- Task categories or tags
- Due dates and reminders
- Dark mode toggle
- Task export functionality
- Drag-and-drop reordering

## License

This project is open source and available under the MIT License.

## Contributing

Feel free to fork this project and submit pull requests for any improvements or bug fixes.

## Support

If you encounter any issues or have questions about the application, please create an issue in the project repository.

---

**Happy task managing!** ✨

### Thanks

- [Vercel](https://vercel.com)
- [Vue 3](https://vuejs.org/)
- [Vite](https://vitejs.dev/)
- [TailwindCSS v4](https://tailwindcss.com/)
