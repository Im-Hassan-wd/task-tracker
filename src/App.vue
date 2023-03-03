<template>
  <div class="container">
    <Header title="Task Tracker" />
    <Tasks :tasks="tasks" />
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
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointement',
        date: 'March 1st at 2:30pm',
        reminder: true
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
