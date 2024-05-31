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
		}
	},
	methods: {
		changeTaskInputValue(val) {
			this.taskInputValue = val
		},
		addTask() {
			const newTask = {
				name: this.taskInputValue,
				completed: false,
			}
			this.taskListArr.push(newTask)
			this.taskInputValue = ''
		},
		removeTask(index) {
			if (this.editableTaskIndex != index) {
				this.taskListArr.splice(index, 1)
			}
		},
		editTask(index) {
			this.taskInputValue = this.taskListArr[index].name
			this.editableTaskIndex = index
		},
		saveTask(index) {
			this.taskListArr[index].name = this.taskInputValue
			this.taskInputValue = ''
			this.editableTaskIndex = -1
		},
		completeTask(index) {
			if (!this.taskListArr[index]['completed']) {
				this.taskListArr[index]['completed'] = true
			} else {
				this.taskListArr[index]['completed'] = false
			}
		},
	},
}
</script>

<style>
#app {
}
</style>
