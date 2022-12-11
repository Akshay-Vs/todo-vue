<template>
  <div class="container">
    <Header title="Task Tracker"/>
    <Task @toggle-reminder="toggleReminder" @delete-task="deleteTask" :task="task"/>
  </div>
</template>

<script>
import Header from "./components/Header"
import Task from "./components/Task"

export default {
  name: 'App',
  components: {
    Header,
    Task
  },
  methods: {
    deleteTask(id) {
      if(confirm("Are you sure you want to delete?")) this.task = this.task.filter((i) => i.id !== id);
    },
    toggleReminder(id) {
      this.task = this.task.map((task)=> task.id === id ? {...task, reminder: !task.reminder} : task);
    }
  },
  data() {
    return {
      task: []
    }
  },
  created() {
    this.task = [
      {
        id: 1,
        text: 'Doctor Appointment',
        day: 'Feb 5th at 2:30pm',
        reminder: true
      },
      {
        id: 2,
        text: 'Meeting at School',
        day: 'Feb 6th at 1:30pm',
        reminder: true
      },
      {
        id: 3,
        text: 'Food Shopping',
        day: 'Feb 5th at 2:30pm',
        reminder: false
      },
      {
        id:4,
        text: 'Programming',
        day: 'Feb 5th at 3:30pm',
        reminder: false
      },
      {
        id:5,
        text: 'HomeWorks',
        day: 'Feb 5th at 4:30pm',
        reminder: true
      }
    ]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
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
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
