<template>
	<input
		type="text"
		@input="changeTaskInputValue($event.target.value)"
		:value="taskInputValue"
		placeholder="Input task"
	/>
	<button v-if="editableTaskIndex == -1" @click="addTask()">Add</button>
	<button v-if="editableTaskIndex !== -1" @click="saveTask(editableTaskIndex)">
		Save
	</button>
</template>

<script>
export default {
	name: 'TaskInput',
	props: {
		changeTaskInputValue: {
			type: Function,
			required: true,
		},
		taskInputValue: {
			type: String,
			required: true,
		},
		addTask: {
			type: Function,
			required: true,
		},
		saveTask: {
			type: Function,
			required: true,
		},
		editableTaskIndex: {
			type: Number,
			required: true,
		},
	},
}
</script>

<style scoped>
input {
	border-radius: 3px;
	border: 0;
	padding: 10px 25px;
	background: #fafafa;
	color: #333;
}

button {
	margin-left: 5px;
	position: relative;
	padding: 10px;
	color: #fff;
	text-transform: uppercase;
	cursor: pointer;
	background: #333;
	border: 0;
	border-radius: 3px;
}
</style>
