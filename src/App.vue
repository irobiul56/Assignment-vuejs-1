<script setup>
import { ref, reactive } from 'vue';

// State
const tasks = reactive([
  { name: 'Task 1', time: 50 },
  { name: 'Task 1', time: 60 },
  { name: 'Task 2', time: 75 },
]);

const isAddTaskPopupOpen = ref(false);
const newTaskName = ref('');
const newTaskTime = ref(0);

// Methods
const openAddTaskPopup = () => {
  isAddTaskPopupOpen.value = true;
};

const closeAddTaskPopup = () => {
  isAddTaskPopupOpen.value = false;
  resetNewTaskForm();
};

const resetNewTaskForm = () => {
  newTaskName.value = '';
  newTaskTime.value = 0;
};

const addTask = () => {
  if (newTaskName.value && newTaskTime.value > 0) {
    tasks.push({ name: newTaskName.value, time: newTaskTime.value });
    closeAddTaskPopup();
  }
};

const removeTask = (index) => {
  tasks.splice(index, 1);
};

</script>

<template>
  <main>
    <section class="place-content">
    <br>
    <button  @click="openAddTaskPopup" type="button" class="focus:outline-none text-white bg-green-700 hover:bg-green-800 focus:ring-4 focus:ring-green-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800">Add</button>

    <br>
    <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
    <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
                <th scope="col" class="px-6 py-3">
                    Sl/No
                </th>
                <th scope="col" class="px-6 py-3">
                    Task
                </th>
                <th scope="col" class="px-6 py-3">
                    Time
                </th>
                <th scope="col" class="px-6 py-3">
                    Action
                </th>
            </tr>
        </thead>
        <tbody>
            <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700" v-for="(task, index) in tasks" :key="index">
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    {{ index+1 }}
                </th>
                <td class="px-6 py-4">
                    {{ task.name }}
                </td>
                <td class="px-6 py-4">
                    {{ task.time }} Minutes
                </td>

                <td class="px-6 py-4">
                  <button class="focus:outline-none text-white bg-red-700 hover:bg-red-800 focus:ring-4 focus:ring-red-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-900" @click="removeTask(index)">Remove</button>
                </td>
            </tr>
        </tbody>
    </table>
</div>
</section>
<!-- Modal -->
<div class="fixed z-10 overflow-y-auto top-0 w-full left-0 popup" v-if="isAddTaskPopupOpen">
  <form @submit.prevent="addTask">
  <div class="flex items-center justify-center min-height-100vh pt-4 px-4 pb-20 text-center sm:block sm:p-0">
    <div class="fixed inset-0 transition-opacity">
      <div class="absolute inset-0 bg-gray-900 opacity-75" />
    </div>
    <span class="hidden sm:inline-block sm:align-middle sm:h-screen">&#8203;</span>
    <div class="inline-block align-center bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full" role="dialog" aria-modal="true" aria-labelledby="modal-headline">
      <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
        <label for="taskName" class="font-medium text-gray-800">Task Name</label>
        <input v-model="newTaskName" id="taskName" type="text" class="text-black w-full rounded bg-gray-100 p-2 mt-2 mb-3">
        <label for="taskTime" class="font-medium text-gray-800">Task Time</label>
        <input v-model="newTaskTime" type="number" id="taskTime" class="text-black w-full rounded bg-gray-100 p-2 mt-2 mb-3" />
      </div>
      <div class="bg-gray-200 px-4 py-3 text-right">
        <button @click="closeAddTaskPopup" type="button" class="py-2 px-4 bg-gray-500 text-white rounded hover:bg-gray-700 mr-2"><i class="fas fa-times"></i> Cancel</button>
        <button type="submit" class="py-2 px-4 bg-blue-500 text-white rounded font-medium hover:bg-blue-700 mr-2 transition duration-500"><i class="fas fa-plus"></i> Add </button>
      </div>
    </div>
  </div>
</form>
</div>
    
  </main>
</template>

<style scoped>

</style>
