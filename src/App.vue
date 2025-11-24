<script setup>
import { computed, onMounted, ref } from 'vue';

const todos = ref([]);
const inputValue = ref('');
const filterStatus = ref('all');
const isDarkMode = ref(true);
const showConfirmModal = ref(false);
const editingId = ref(null);
const editText = ref('');

const STORAGE_KEY = 'vue-todos';
const THEME_KEY = 'vue-todos-theme';

onMounted(() => {
    loadTheme();
    loadTodos();
});

const loadTheme = () => {
    const stored = localStorage.getItem(THEME_KEY);
    if (stored !== null) {
        isDarkMode.value = JSON.parse(stored);
    }
};

const saveTheme = () => {
    localStorage.setItem(THEME_KEY, JSON.stringify(isDarkMode.value));
};

const toggleTheme = () => {
    isDarkMode.value = !isDarkMode.value;
    saveTheme();
};

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

const changeItemValue = (id, key, value) => {
    const todo = todos.value.find((t) => t.id === id);

    if (!todo) {
        return;
    }

    todo[key] = value;
    saveTodos();
};

const makeAsCompleted = (id) => {
    changeItemValue(id, 'completed', true);
};

const makeAsUncompleted = (id) => {
    changeItemValue(id, 'completed', false);
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

const openConfirmModal = () => {
    showConfirmModal.value = true;
};

const confirmClearCompleted = () => {
    clearCompleted();
    showConfirmModal.value = false;
};

const cancelClearCompleted = () => {
    showConfirmModal.value = false;
};

const startEditing = (todo) => {
    editingId.value = todo.id;
    editText.value = todo.text;
};

const saveEdit = (id) => {
    const todo = todos.value.find((t) => t.id === id);
    if (todo && editText.value.trim()) {
        todo.text = editText.value.trim();
        todo.completed = false;
        saveTodos();
        editingId.value = null;
        editText.value = '';
    }
};

const cancelEdit = () => {
    editingId.value = null;
    editText.value = '';
};

const filteredTodos = computed(() => {
    if (filterStatus.value === 'completed') {
        return todos.value.filter((t) => t.completed);
    }

    if (filterStatus.value === 'pending') {
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
    <div
        :class="[
            'min-h-screen py-8 px-4 transition-colors',
            {
                'bg-linear-to-br from-gray-900 to-gray-800': isDarkMode,
                'bg-linear-to-br from-blue-50 to-indigo-100': !isDarkMode,
            },
        ]"
    >
        <div class="max-w-2xl mx-auto">
            <!-- Header -->
            <div
                :class="[
                    'sticky top-0 z-20 text-center mb-8 py-4 -mx-4 px-4 transition-colors',
                    {
                        'bg-linear-to-br from-gray-900 to-gray-800': isDarkMode,
                        'bg-linear-to-br from-blue-50 to-indigo-100': !isDarkMode,
                    },
                ]"
            >
                <div class="flex items-center justify-center gap-4">
                    <h1
                        :class="['text-4xl font-bold mb-2', { 'text-white': isDarkMode, 'text-gray-800': !isDarkMode }]"
                    >
                        Another TODO App
                    </h1>
                    <button
                        @click="toggleTheme"
                        :class="[
                            'px-3 py-2 rounded-lg transition-colors',
                            {
                                'bg-gray-700 text-white hover:bg-gray-600': isDarkMode,
                                'bg-white text-gray-800 hover:bg-gray-100': !isDarkMode,
                            },
                        ]"
                        :title="isDarkMode ? 'Switch to light mode' : 'Switch to dark mode'"
                    >
                        {{ isDarkMode ? '☀️' : '🌙' }}
                    </button>
                </div>
                <p :class="{ 'text-gray-300': isDarkMode, 'text-gray-600': !isDarkMode }">
                    Manage your tasks efficiently
                </p>
            </div>

            <!-- Stats -->
            <div class="grid grid-cols-3 gap-4 mb-6">
                <div
                    :class="[
                        'rounded-lg shadow p-4 text-center',
                        { 'bg-gray-800': isDarkMode, 'bg-white': !isDarkMode },
                    ]"
                >
                    <p class="text-2xl font-bold text-blue-600">{{ stats.total }}</p>
                    <p :class="{ 'text-gray-300': isDarkMode, 'text-gray-600': !isDarkMode }" class="text-sm">
                        Total Tasks
                    </p>
                </div>
                <div
                    :class="[
                        'rounded-lg shadow p-4 text-center',
                        { 'bg-gray-800': isDarkMode, 'bg-white': !isDarkMode },
                    ]"
                >
                    <p class="text-2xl font-bold text-green-600">{{ stats.completed }}</p>
                    <p :class="{ 'text-gray-300': isDarkMode, 'text-gray-600': !isDarkMode }" class="text-sm">
                        Completed
                    </p>
                </div>
                <div
                    :class="[
                        'rounded-lg shadow p-4 text-center',
                        { 'bg-gray-800': isDarkMode, 'bg-white': !isDarkMode },
                    ]"
                >
                    <p class="text-2xl font-bold text-orange-600">{{ stats.pending }}</p>
                    <p :class="{ 'text-gray-300': isDarkMode, 'text-gray-600': !isDarkMode }" class="text-sm">
                        Pending
                    </p>
                </div>
            </div>

            <div
                :class="[
                    'sticky top-20 z-10 w-full px-4 py-2 rounded-lg mb-6 backdrop-blur-sm',
                    { 'bg-gray-800/95': isDarkMode, 'bg-white/95': !isDarkMode },
                ]"
            >
                <div class="flex flex-col gap-2 mb-6">
                    <!-- Input Section -->
                    <div
                        :class="[
                            'rounded-lg shadow-md p-6 mb-6',
                            { 'bg-gray-800': isDarkMode, 'bg-white': !isDarkMode },
                        ]"
                    >
                        <div class="flex gap-2">
                            <input
                                v-model="inputValue"
                                @keydown="handleKeyDown"
                                type="text"
                                placeholder="Add a new task..."
                                :class="[
                                    'flex-1 px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500',
                                    {
                                        'bg-gray-700 border-gray-600 text-white placeholder-gray-400': isDarkMode,
                                        'bg-white border-gray-300 text-gray-900 placeholder-gray-500': !isDarkMode,
                                    },
                                ]"
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
                                'px-4 py-2 rounded-lg font-medium transition-colors capitalize cursor-pointer',
                                {
                                    'bg-blue-600 text-white': filterStatus === status,
                                    'bg-gray-700 text-gray-300 hover:bg-gray-600 border border-gray-600':
                                        filterStatus !== status && isDarkMode,
                                    'bg-white text-gray-700 hover:bg-gray-100 border border-gray-300':
                                        filterStatus !== status && !isDarkMode,
                                },
                            ]"
                        >
                            <span>
                                {{ status }}
                            </span>
                            <span v-if="status === 'all'" class="text-xs">({{ stats?.total || 0 }})</span>

                            <span v-if="status in stats" class="text-xs">({{ stats[status] }})</span>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Todo List -->
            <div class="space-y-2">
                <div
                    v-if="filteredTodos.length === 0"
                    :class="[
                        'rounded-lg shadow p-8 text-center',
                        { 'bg-gray-800 text-gray-400': isDarkMode, 'bg-white text-gray-500': !isDarkMode },
                    ]"
                >
                    <p v-if="todos.length === 0">No tasks yet. Add one to get started!</p>
                    <p v-else>No tasks found in this filter.</p>
                </div>

                <div
                    v-for="todo in filteredTodos"
                    :key="todo.id"
                    :class="[
                        'rounded-lg shadow p-4 flex items-center gap-3 hover:shadow-md transition-shadow',
                        { 'bg-gray-800': isDarkMode, 'bg-white': !isDarkMode },
                    ]"
                >
                    <input
                        type="checkbox"
                        :checked="todo.completed"
                        @change="toggleTodo(todo.id)"
                        :disabled="editingId === todo.id"
                        class="w-5 h-5 text-blue-600 rounded focus:ring-2 focus:ring-blue-500 cursor-pointer disabled:opacity-50"
                    />

                    <!-- Display mode -->
                    <span
                        v-if="editingId !== todo.id"
                        :class="[
                            'flex-1 text-left',
                            {
                                'line-through text-gray-500': todo.completed && isDarkMode,
                                'line-through text-gray-400': todo.completed && !isDarkMode,
                                'text-gray-200': !todo.completed && isDarkMode,
                                'text-gray-800': !todo.completed && !isDarkMode,
                            },
                        ]"
                    >
                        {{ todo.text }}
                    </span>

                    <!-- Edit mode -->
                    <input
                        v-if="editingId === todo.id"
                        v-model="editText"
                        type="text"
                        class="flex-1 px-3 py-1 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                        :class="{
                            'bg-gray-700 border-gray-600 text-white placeholder-gray-400': isDarkMode,
                            'bg-white border-gray-300 text-gray-900 placeholder-gray-500': !isDarkMode,
                        }"
                        @keydown.enter="saveEdit(todo.id)"
                        @keydown.escape="cancelEdit"
                        autofocus
                    />

                    <!-- Action buttons -->
                    <div v-if="editingId !== todo.id" class="flex gap-2 buttons-group">
                        <button
                            @click.prevent.stop="startEditing(todo)"
                            v-if="!todo?.completed"
                            :class="[
                                'px-3 py-1 rounded transition-colors text-sm font-medium',
                                {
                                    'text-blue-400 hover:bg-blue-900/30': isDarkMode,
                                    'text-blue-600 hover:bg-blue-50': !isDarkMode,
                                },
                            ]"
                        >
                            Edit
                        </button>
                        <button
                            v-if="todo.completed"
                            @click.prevent.stop="makeAsUncompleted(todo.id)"
                            :class="[
                                'px-3 py-1 rounded transition-colors text-sm font-medium',
                                {
                                    'text-yellow-400 hover:bg-yellow-900/30': isDarkMode,
                                    'text-yellow-600 hover:bg-yellow-50': !isDarkMode,
                                },
                            ]"
                        >
                            Undone
                        </button>
                        <button
                            @click.prevent.stop="deleteTodo(todo.id)"
                            :class="[
                                'px-3 py-1 rounded transition-colors text-sm font-medium',
                                {
                                    'text-red-400 hover:bg-red-900/30': isDarkMode,
                                    'text-red-600 hover:bg-red-50': !isDarkMode,
                                },
                            ]"
                        >
                            Delete
                        </button>
                    </div>

                    <!-- Save/Cancel buttons (edit mode) -->
                    <div v-else class="flex gap-2 buttons-group">
                        <button
                            @click="saveEdit(todo.id)"
                            class="px-3 py-1 bg-green-600 text-white rounded transition-colors text-sm font-medium hover:bg-green-700"
                        >
                            Save
                        </button>
                        <button
                            @click="cancelEdit"
                            :class="[
                                'px-3 py-1 rounded transition-colors text-sm font-medium',
                                {
                                    'bg-gray-700 text-white hover:bg-gray-600': isDarkMode,
                                    'bg-gray-300 text-gray-900 hover:bg-gray-400': !isDarkMode,
                                },
                            ]"
                        >
                            Cancel
                        </button>
                    </div>
                </div>
            </div>

            <!-- Clear Completed Button -->
            <div v-if="stats.completed > 0" class="mt-6 text-center">
                <button
                    @click="openConfirmModal"
                    :class="[
                        'px-4 py-2 rounded-lg transition-colors font-medium',
                        { 'text-red-400 hover:bg-red-900/30': isDarkMode, 'text-red-600 hover:bg-red-50': !isDarkMode },
                    ]"
                >
                    Clear {{ stats.completed }} Completed Task{{ stats.completed !== 1 ? 's' : '' }}
                </button>
            </div>
        </div>

        <!-- Confirmation Modal -->
        <div v-if="showConfirmModal" class="fixed inset-0 bg-black/50 flex items-center justify-center z-50 p-4">
            <div
                :class="[
                    'rounded-lg shadow-xl p-6 max-w-sm w-full',
                    { 'bg-gray-800': isDarkMode, 'bg-white': !isDarkMode },
                ]"
            >
                <h2 :class="['text-xl font-bold mb-4', { 'text-white': isDarkMode, 'text-gray-900': !isDarkMode }]">
                    Clear Completed Tasks?
                </h2>
                <p :class="['mb-6', { 'text-gray-300': isDarkMode, 'text-gray-600': !isDarkMode }]">
                    Are you sure you want to delete {{ stats.completed }} completed task{{
                        stats.completed !== 1 ? 's' : ''
                    }}? This action cannot be undone.
                </p>
                <div class="flex gap-3 justify-end">
                    <button
                        @click="cancelClearCompleted"
                        :class="[
                            'px-4 py-2 rounded-lg font-medium transition-colors',
                            {
                                'bg-gray-700 text-white hover:bg-gray-600': isDarkMode,
                                'bg-gray-200 text-gray-900 hover:bg-gray-300': !isDarkMode,
                            },
                        ]"
                    >
                        Cancel
                    </button>
                    <button
                        @click="confirmClearCompleted"
                        class="px-4 py-2 bg-red-600 text-white rounded-lg font-medium hover:bg-red-700 transition-colors"
                    >
                        Delete
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
