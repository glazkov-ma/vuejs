<template>
	<div class="task" v-for="(el, index) in taskListArr" :key="index">
		<span :class="{ completed: el.completed }">{{ el.name }}</span>
		<div class="actions">
			<button class="action-button" @click="removeTask(index)">
				<font-awesome-icon class="fa-icon trash-alt" icon="trash-alt" />
			</button>
			<button class="action-button" @click="editTask(index)">
				<font-awesome-icon class="fa-icon edit" icon="edit" />
			</button>
			<button class="action-button" @click="completeTask(index)">
				<font-awesome-icon class="fa-icon check" icon="check" />
			</button>
		</div>
	</div>
</template>

<script>
export default {
	name: 'TaskList',
	props: {
		taskListArr: {
			type: Array,
			required: true,
		},
		removeTask: {
			type: Function,
			required: true,
		},
		editTask: {
			type: Function,
			required: true,
		},
		completeTask: {
			type: Function,
			required: true,
		},
	},
}
</script>

<style scoped>
.task {
	display: flex;
	align-items: center;
	text-align: left;
	justify-content: space-between;
	width: 50%;
	background: #f9f9f9;
	margin: 0 auto;
	padding: 10px;
	border-radius: 5px;
	box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	margin-top: 10px;
}

.actions {
	display: flex;
	gap: 10px;
}

.action-button {
	background: none;
	border: none;
	cursor: pointer;
	padding: 5px;
	border-radius: 50%;
	transition: background-color 0.3s;
}

.action-button:hover {
	background-color: #e0e0e0;
}

.action-button:focus {
	outline: none;
}

.action-button .fa-icon {
	font-size: 1.2em;
	color: #333333;
}

.fa-icon.trash-alt {
	color: #770000;
}

.fa-icon.edit {
	color: #6d5000;
}

.fa-icon.check {
	color: #00770a;
}

.completed {
	text-decoration: line-through;
}
</style>
