<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask" />
    <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks" />
    <router-view></router-view>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header"
import Tasks from "./components/Tasks"
import AddTask from "./components/AddTask"
import Footer from "./components/Footer"

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
    Footer,
  },
  data() {
    return {
      tasks: [],
      showAddTask: true
    }
  },
  methods: {
    async deleteTask(id) {
      if(confirm('Are you sure you want to delete this task??')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE'
        })

        res.status === 200 ? (this.tasks = this.tasks.filter(task => task.id !== id)) : alert('Error deleting task')
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const updatedTask = {...taskToToggle, reminder: !taskToToggle.reminder}

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updatedTask)
      })

      const data = await res.json()

      this.tasks = this.tasks.map(task => task.id === id ? {...task, reminder: data.reminder} : task)
    },
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })

      const data = await res.json()

      this.tasks = [...this.tasks, task]
    },
    toggleAddTasks() {
      this.showAddTask = !this.showAddTask
    },
    async fetchTasks() {
      const res = await fetch("api/tasks")
      const data = await res.json()

      return data
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`)
      const data = await res.json()

      return data
    },
  },
  async created() {
    this.tasks = await this.fetchTasks()
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800;900&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

body {
  color: #333;
}

.container {
  max-width: 700px;
  margin: 32px auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 24px;
  border-radius: 12px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 16px;

}
</style>
