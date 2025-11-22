<script setup>
import {
    computed,
    onMounted,
    ref,
} from 'vue';

const todos = ref([]);
const inputValue = ref('');
const filterStatus = ref('all');

const STORAGE_KEY = 'vue-todos';

onMounted(() => {
    loadTodos();
});

const loadTodos = () => {
    const stored = localStorage.getItem(STORAGE_KEY);
    if (stored) {
        todos.value = JSON.parse(stored);
    }
};

const saveTodos = () => {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todos.value));
};

const addTodo = () => {
    if (inputValue.value.trim()) {
        todos.value.push({
            id: Date.now(),
            text: inputValue.value,
            completed: false,
            createdAt: new Date().toISOString(),
        });
        inputValue.value = '';
        saveTodos();
    }
};

const toggleTodo = (id) => {
    const todo = todos.value.find((t) => t.id === id);
    if (todo) {
        todo.completed = !todo.completed;
        saveTodos();
    }
};

const deleteTodo = (id) => {
    todos.value = todos.value.filter((t) => t.id !== id);
    saveTodos();
};

const clearCompleted = () => {
    todos.value = todos.value.filter((t) => !t.completed);
    saveTodos();
};

const filteredTodos = computed(() => {
    if (filterStatus.value === 'completed') {
        return todos.value.filter((t) => t.completed);
    } else if (filterStatus.value === 'pending') {
        return todos.value.filter((t) => !t.completed);
    }
    return todos.value;
});

const stats = computed(() => ({
    total: todos.value.length,
    completed: todos.value.filter((t) => t.completed).length,
    pending: todos.value.filter((t) => !t.completed).length,
}));

const handleKeyDown = (event) => {
    if (event.key === 'Enter') {
        addTodo();
    }
};
</script>

<template>
    <div class="min-h-screen bg-linear-to-br from-blue-50 to-indigo-100 py-8 px-4">
        <div class="max-w-2xl mx-auto">
            <!-- Header -->
            <div class="text-center mb-8">
                <h1 class="text-4xl font-bold text-gray-800 mb-2">Another TODO App</h1>
                <p class="text-gray-600">Manage your tasks efficiently</p>
            </div>

            <!-- Stats -->
            <div class="grid grid-cols-3 gap-4 mb-6">
                <div class="bg-white rounded-lg shadow p-4 text-center">
                    <p class="text-2xl font-bold text-blue-600">{{ stats.total }}</p>
                    <p class="text-gray-600 text-sm">Total Tasks</p>
                </div>
                <div class="bg-white rounded-lg shadow p-4 text-center">
                    <p class="text-2xl font-bold text-green-600">{{ stats.completed }}</p>
                    <p class="text-gray-600 text-sm">Completed</p>
                </div>
                <div class="bg-white rounded-lg shadow p-4 text-center">
                    <p class="text-2xl font-bold text-orange-600">{{ stats.pending }}</p>
                    <p class="text-gray-600 text-sm">Pending</p>
                </div>
            </div>

            <!-- Input Section -->
            <div class="bg-white rounded-lg shadow-md p-6 mb-6">
                <div class="flex gap-2">
                    <input
                        v-model="inputValue"
                        @keydown="handleKeyDown"
                        type="text"
                        placeholder="Add a new task..."
                        class="flex-1 px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                    />
                    <button
                        @click="addTodo"
                        class="px-6 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors font-medium"
                    >
                        Add
                    </button>
                </div>
            </div>

            <!-- Filter Buttons -->
            <div class="flex gap-2 mb-6">
                <button
                    v-for="status in ['all', 'pending', 'completed']"
                    :key="status"
                    @click="filterStatus = status"
                    :class="[
                        'px-4 py-2 rounded-lg font-medium transition-colors capitalize',
                        filterStatus === status
                            ? 'bg-blue-600 text-white'
                            : 'bg-white text-gray-700 hover:bg-gray-100 border border-gray-300',
                    ]"
                >
                    {{ status }}
                </button>
            </div>

            <!-- Todo List -->
            <div class="space-y-2">
                <div v-if="filteredTodos.length === 0" class="bg-white rounded-lg shadow p-8 text-center text-gray-500">
                    <p v-if="todos.length === 0">No tasks yet. Add one to get started!</p>
                    <p v-else>No tasks found in this filter.</p>
                </div>

                <div
                    v-for="todo in filteredTodos"
                    :key="todo.id"
                    class="bg-white rounded-lg shadow p-4 flex items-center gap-3 hover:shadow-md transition-shadow"
                >
                    <input
                        type="checkbox"
                        :checked="todo.completed"
                        @change="toggleTodo(todo.id)"
                        class="w-5 h-5 text-blue-600 rounded focus:ring-2 focus:ring-blue-500 cursor-pointer"
                    />
                    <span
                        :class="['flex-1 text-left', todo.completed ? 'line-through text-gray-400' : 'text-gray-800']"
                    >
                        {{ todo.text }}
                    </span>
                    <button
                        @click="deleteTodo(todo.id)"
                        class="px-3 py-1 text-red-600 hover:bg-red-50 rounded transition-colors text-sm font-medium"
                    >
                        Delete
                    </button>
                </div>
            </div>

            <!-- Clear Completed Button -->
            <div v-if="stats.completed > 0" class="mt-6 text-center">
                <button
                    @click="clearCompleted"
                    class="px-4 py-2 text-red-600 hover:bg-red-50 rounded-lg transition-colors font-medium"
                >
                    Clear {{ stats.completed }} Completed Task{{ stats.completed !== 1 ? 's' : '' }}
                </button>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
