<template>
	<p>Task Manager</p>
	<TaskInput
		:changeTaskInputValue="changeTaskInputValue"
		:taskInputValue="taskInputValue"
		:addTask="addTask"
		:saveTask="saveTask"
		:editableTaskIndex="editableTaskIndex"
	/>
	<p v-show="taskListArr.length > 0">All tasks:</p>
	<TaskList
		:taskListArr="taskListArr"
		:removeTask="removeTask"
		:editTask="editTask"
		:completeTask="completeTask"
		v-if="taskListArr.length > 0"
	/>
</template>

<script>
import TaskInput from './components/TaskInput.vue'
import TaskList from './components/TaskList.vue'

export default {
	name: 'App',
	components: {
		TaskInput,
		TaskList,
	},
	data() {
		return {
			taskInputValue: '',
			taskListArr: [],
			editableTaskIndex: -1,
			currentTaskId: -1,
		}
	},
	methods: {
		changeTaskInputValue(val) {
			this.taskInputValue = val
		},
		addTask() {
			this.currentTaskId++
			const newTask = {
				id: this.currentTaskId,
				name: this.taskInputValue,
				completed: false,
			}
			this.taskListArr.push(newTask)
			this.taskInputValue = ''
		},
		removeTask(index) {
			if (this.editableTaskIndex != index) {
				this.taskListArr = this.taskListArr.filter(task => task.id !== index)
			}
		},
		editTask(index) {
			const task = this.getTaskById(index)
			this.taskInputValue = task.name
			this.editableTaskIndex = index
		},
		saveTask(index) {
			const task = this.getTaskById(index)
			task.name = this.taskInputValue
			this.taskInputValue = ''
			this.editableTaskIndex = -1
		},
		completeTask(index) {
			const task = this.getTaskById(index)
			if (!task.completed) {
				task.completed = true
			} else {
				task.completed = false
			}
		},
		getTaskById(id) {
			return this.taskListArr.find(task => task.id === id)
		},
	},
}
</script>

<style>
#app {
}
</style>
