<script setup>
const props = defineProps({
	text: {
		type: String,
		required: true,
		default: "Текст Отсутствует",
	},
	id: {
		type: Number,
		required: true,
		default: 0,
	},
	isCompleted: {
		type: Boolean,
		required: true,
		default: false,
	},
})

const emit = defineEmits(["setCompletion", "deleteTask"])

const setCompletion = () => {
	emit("setCompletion", props.id)
}

const deleteTask = () => {
	emit("deleteTask", props.id)
}
</script>

<template>
	<div class="task" :class="{ 'task--completed': isCompleted }">
		<input :placeholder="text" @click="setCompletion" type="text" readonly />
		<button @click="deleteTask">x</button>
	</div>
</template>

<style scoped>
.task {
	display: flex;
	width: 100%;

	margin-bottom: 8px;
}

.task input {
	flex-grow: 1;
	padding: 0.5rem;

	font-family: "Nunito", sans-serif;
	font-style: normal;
	font-weight: 400;
	font-size: 1rem;
	color: #0a0a0a;

	border: 1px solid #d9d9d9;
	border-radius: 1px;
	outline: none;
	background-color: #f2f2f2;
	box-shadow: inset 0 1px 2px hsla(0, 0%, 4%, 0.1);

	transition: all 0.2s ease;
	cursor: pointer;
}

.task input::placeholder {
	font-family: "Nunito", sans-serif;
	font-style: normal;
	font-weight: 400;
	font-size: 1rem;
	color: #0a0a0a;
}

.task input:hover,
.task input:focus,
.task input:active {
	background-color: rgba(0, 0, 0, 0.1);
	border-color: rgba(0, 0, 0, 0.15);
}

.task button {
	height: 45px;
	width: 42px;
	padding: 0.85em 1em;

	font-family: "Nunito", sans-serif;
	text-align: center;
	font-size: 0.9rem;
	line-height: 1;
	color: #fefefe;

	border: 1px solid transparent;
	background-color: #ec5840;

	display: block;
	cursor: pointer;

	transition: all 0.2s ease;
}

.task button:hover,
.task button:focus,
.task button:active {
	background-color: #da3116;
}

.task--completed input {
	text-decoration: line-through;
	background-color: rgba(0, 128, 0, 0.15);
	border-color: rgb(242 242 242);
}

.task--completed input:hover,
.task--completed input:focus,
.task--completed input:active {
	background-color: rgba(0, 128, 0, 0.25);
	border-color: rgba(0, 128, 0, 0.3);
}
</style>
