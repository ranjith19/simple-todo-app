<template>
  <div id="app">
    <h1>Simple To-Do App</h1>
    <div>
      <input v-model="newTask.name" type="text" placeholder="New task">
      <input v-model="newTask.deadline" type="date" placeholder="Deadline">
      <button
      class="add-task-button"
      :disabled="newTask.name === '' || newTask.deadline === ''"
       @click="addTask">Add Task</button>
    </div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span :class="{ done: task.done }">{{ task.name }} - {{ task.deadline }}</span>
        <button class="mark-done-button" @click="markAsDone(index)">Mark as Done</button>
        <button class="delete-button" @click="deleteTask(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: {
        name: '',
        deadline: '',
        done: false,
      },
      tasks: []
    }
  },
  methods: {
    addTask() {
      if (this.newTask.name !== '' && this.newTask.deadline !== '') {
        this.tasks.push({ ...this.newTask });
        this.newTask.name = '';
        this.newTask.deadline = '';
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    markAsDone(index) {
      this.tasks[index].done = !this.tasks[index].done;
    }
  }
}
</script>




<style scoped>
  #app {
    font-family: Arial, sans-serif;
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
    border-radius: 5px;
    background-color: #f5f5f5;
  }

  h1 {
    color: #333;
    text-align: center;
  }

  div {
    margin-bottom: 20px;
    justify-content: center;
    align-items: center;
  }

  ul {
    padding: 0;
  }

  li {
    background-color: #fff;
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 3px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  span {
    font-size: 18px;
    flex-grow: 1;
  }

  .done {
    text-decoration: line-through;
    color: #999;
  }

  button {
    padding: 5px 10px;
    margin-left: 10px;
    border-radius: 3px;
    border: none;
    color: #fff;
    cursor: pointer;
  }

  button:hover {
    opacity: 0.9;
  }

  input[type="text"],
  input[type="date"] {
    margin-right: 10px;
    padding: 5px;
    border-radius: 3px;
    border: 1px solid #ddd;
  }

  .add-task-button {
    background-color: #2ecc71;
  }

  .add-task-button:disabled {
    background-color: #ddd;
    cursor: not-allowed;
  }

  .mark-done-button {
    background-color: #3498db;
  }

  .delete-button {
    background-color: #e74c3c;
  }
</style>
