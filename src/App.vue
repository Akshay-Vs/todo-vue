<template>
	<div class="container">
		<Header title="Task Tracker" @show-add-task="toggleAddTask" :AddTask="showAddTask" />
		<div v-show="showAddTask">
			<AddTask @add-new="addTask" />
		</div>
		<Task @toggle-reminder="toggleReminder" @delete-task="deleteTask" :task="task" />
		<router-view></router-view>
		<Footer />
	</div>
</template>

<script>
import Header from "./components/Header"
import Task from "./components/Task"
import AddTask from "./components/AddTask"
import Footer from "./components/footer"
export default {
	name: 'App',
	components: {
		Header,
		Footer,
		Task,
		AddTask
	},
	methods:
	{
		toggleAddTask() {
			this.showAddTask = !this.showAddTask
		},

		async toggleReminder(id) {

			const taskToToggle = await this.fetchTask(id)
			const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder }

			const res = await fetch(`api/tasks/${id}`, {
				method: 'PUT',
				headers: {
					'Content-type': 'application/json'
				},
				body: JSON.stringify(updTask)
			})

			const data = await res.json()

			this.task = this.task.map((task) => task.id === id ? { ...task, reminder: data.reminder } : task);
		},
		async fetchTasks() {
			const res = await fetch('api/tasks')
			const data = await res.json()
			return data
		},

		async fetchTask(id) {
			const res = await fetch(`api/tasks/${id}`)
			const data = await res.json()
			return data
		},

		async addTask(task) {
			const res = await fetch('api/tasks', {
				method: 'POST',
				headers: {
					'Content-type': 'application/json'
				},
				body: JSON.stringify(task)
			})

			const data = await res.json()
			this.task = [...this.task, data]
		},
		async deleteTask(id) {

			const res = await fetch(`api/tasks/${id}`, {
				method: 'DELETE'
			})
			if (confirm("Are you sure you want to delete?")) res.status === 200 ? (this.task = this.task.filter((i) => i.id !== id)) : alert("Failed to delete task");

		},

	},

	async created() {
		this.task = await this.fetchTasks()
	},


	data() {
		return {
			showAddTask: false,
			task: []
		}
	},


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
	width: 150px;
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
	transition: 500ms;
}

.btn:focus {
	outline: none;
}

.btn:active {
	transform: scale(0.98);
	transition: 500ms;
}

.btn-block {
	display: block;
	width: 100%;
}
</style>
