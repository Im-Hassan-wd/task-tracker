<template>
  <div class="container">
    <Header title="Task Tracker" />
    <Tasks @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks" />
  </div>
</template>

<script>
import Header from "./components/Header"
import Tasks from "./components/Tasks"

export default {
  name: "App",
  components: {
    Header,
    Tasks,
  },
  data() {
    return {
      tasks: []
    }
  },
  methods: {
    deleteTask(id) {
      if(confirm('Are you sure you want to delete this task??')) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map(task => task.id === id ? {...task, reminder: !task.reminder} : task)
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointement',
        date: 'March 1st at 2:30pm',
        reminder: false
      },
      {
        id: 2,
        text: 'Meeting at School',
        date: 'March 3rd at 5:30am',
        reminder: true
      },
      {
        id: 3,
        text: 'Play MiniMilitia',
        date: 'Every goddem day',
        reminder: true
      }
    ]
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
