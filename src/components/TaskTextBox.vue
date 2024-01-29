<template>
  <div class="task-text-box">
    <input
      v-model="task"
      type="text"
      id="name"
      name="name"
      placeholder="Add a task"
      @keyup.enter="isButtonDisabled ? null : addTask()"
      required
    />

    <input
      :disabled="isButtonDisabled"
      type="button"
      value="Add Task"
      :class="{ 'task-button-disabled': isButtonDisabled }"
      class="task-button"
      @click="addTask()"
    />

    <ul>
      <li v-for="(t, index) in taskList" class="task-item" :key="index">
        <p :class="{ strikethrough: t.checked }">{{ t.task }}</p>
        <div class="actions">
          <v-icon @click="checkTask(t)" color="blue" class="check-action"
            >mdi-checkbox-marked-circle-outline</v-icon
          >
          <v-icon @click="removeTask(t)" class="delete-action" color="red">
            mdi-delete-forever
          </v-icon>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const taskList = ref([]);

if (localStorage.taskList) {
  taskList.value = JSON.parse(localStorage.taskList.split(","));
}

const task = ref("");
const isButtonDisabled = computed(() => task.value.length < 3);

const addTask = () => {
  taskList.value.push({ task: task.value, checked: false });
  task.value = "";

  localStorage.setItem("taskList", JSON.stringify(taskList.value));
};

const checkTask = (t) => {
  t.checked = !t.checked;
  localStorage.setItem("taskList", JSON.stringify(taskList.value));
};

const removeTask = (task) => {
  taskList.value = taskList.value.filter((item) => item !== task);
  localStorage.setItem("taskList", JSON.stringify(taskList.value));
};
</script>

<style lang="scss" scoped>
.task-text-box {
  margin: 5px 0 5px 0;
  text-align: center;
}

input[type="text"] {
  border: 1px solid $primary-900;
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
}

.task-button {
  width: 100%;
  height: 60px;
  color: $primary-800;
  background-color: $primary-600;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.task-button-disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

ul {
  list-style-type: none;
  margin: 0;
  margin-top: 10px;
  padding: 0;
  height: 360px;
  overflow-y: auto;
  border-top: 1px solid $primary-600;
}

ul > li {
  font-size: 16px;
  color: $accent-400;
  font-weight: 500;
  height: 40px;
  line-height: 40px;
  text-align: left;
  border-bottom: 1px solid $primary-600;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.actions {
  display: inherit;
  gap: 10px;
}

.strikethrough {
  text-decoration: line-through;
}
</style>
