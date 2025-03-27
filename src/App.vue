<script setup>
import { computed, ref } from "vue"
import TodoTask from "./components/TodoTask.vue"

const tasks = ref([
	{
		id: 0,
		text: "Make todo list",
		isCompleted: true,
	},
	{
		id: 1,
		text: "Go skydiving",
		isCompleted: false,
	},
	{
		id: 2,
		text: "Go run",
		isCompleted: false,
	},
])

const completedTasksCount = computed(() => {
	return tasks.value.filter(task => !task.isCompleted).length
})

const newTask = ref("")

const deleteTask = id => {
	tasks.value = tasks.value.filter(task => task.id !== id)

	for (let i = 0; i < tasks.value.length; i++) {
		tasks.value[i].id = i
	}
}

const setCompletion = id => {
	tasks.value.find(task => task.id === id).isCompleted = !tasks.value.find(
		task => task.id === id
	).isCompleted
}

const deleteCompletedTasks = () => {
	tasks.value = tasks.value.filter(task => !task.isCompleted)

	for (let i = 0; i < tasks.value.length; i++) {
		tasks.value[i].id = i
	}
}

const deleteAllTasks = () => {
	tasks.value.length = 0
}

const addTask = () => {
	if (newTask.value === "") return
	tasks.value.push({
		id: tasks.value.length + 1,
		text: newTask.value,
		isCompleted: false,
	})

	for (let i = 0; i < tasks.value.length; i++) {
		tasks.value[i].id = i
		// console.log(i)
	}

	newTask.value = ""
}
</script>

<template>
	<div class="container-wr">
		<div class="container">
			<div class="counter">
				<p>Tasks</p>
				<div>
					(
					<span>{{ completedTasksCount }}</span>
					)
				</div>
			</div>

			<form @submit.prevent="addTask" class="create-task">
				<input
					v-model="newTask"
					type="text"
					name="name"
					placeholder="New task"
				/>
				<button>+ Add</button>
			</form>

			<div class="clear">
				<button @click="deleteCompletedTasks" class="clear__completed">
					<svg x="0px" y="0px" width="100" height="100" viewBox="0,0,256,256">
						<g
							fill="none"
							fill-rule="nonzero"
							stroke="none"
							stroke-width="1"
							stroke-linecap="butt"
							stroke-linejoin="miter"
							stroke-miterlimit="10"
							stroke-dasharray=""
							stroke-dashoffset="0"
							font-family="none"
							font-weight="none"
							font-size="none"
							text-anchor="none"
							style="mix-blend-mode: normal"
						>
							<g transform="scale(0.5,0.5)">
								<path
									d="M424.3,180c-1,-1.2 -1.5,-2.8 -1.5,-4.3c-14.8,-26.1 -15.7,-58 -30.5,-84.1c-41.7,23.4 -70.2,65.1 -97.4,103.1c-16.4,22.9 -31.1,46.4 -44.6,71.1c-13.6,24.8 -26.8,49.9 -42,73.8c-2.2,3.4 -7.9,5 -10.3,0.7c-7.2,-13.3 -15.3,-26.2 -24.6,-38.2c-8,-10.3 -17.1,-19.5 -25.3,-29.6c-12.7,-15.7 -26.3,-34.5 -43.9,-45.4c-6.4,21 -13.9,41.8 -17.2,63.6c24.6,15.9 43.4,38.9 61.5,61.6c21.2,26.6 43.1,52 66.9,76.3c15.4,-20.1 26,-43.5 38.8,-65.3c15.1,-25.7 32.7,-49.4 51.4,-72.6c18.7,-23.2 40.3,-43.7 62,-63.9c10.2,-9.5 22.2,-17.3 33.1,-26c8.2,-6.6 16.2,-13.4 23.7,-20.7c0,0.1 0,0 -0.1,-0.1z"
									fill="#fefefe"
								></path>
								<path
									d="M436.2,170.3h-2.8c-16.3,-27.7 -16.2,-62.6 -34,-89.9c-1.9,-3 -5.4,-3.1 -8.3,-1.6c-45.6,23.1 -76.2,67.7 -105.2,108.1c-16.6,23.2 -31.6,47 -45.4,72c-12.3,22.3 -24.1,44.8 -37.4,66.6c-6,-10.4 -12.6,-20.4 -19.9,-29.9c-8.2,-10.8 -17.8,-20.3 -26.3,-30.8c-15.2,-18.7 -31.4,-40.9 -53.7,-51.5c-3.7,-1.8 -7.4,0.5 -8.5,4.2c-6.8,23.7 -15.8,47 -19.5,71.4c0,0.1 0,0.2 0,0.4c-2,2.7 -2.2,7.1 1.6,9.4c26.5,15.6 46,40.8 64.9,64.6c22,27.7 45.2,54.1 70.2,79.1c2.3,2.3 6.4,1.8 8.4,-0.5c17.2,-20.6 28.7,-45 41.8,-68.2c14.7,-25.9 32,-50.3 51.1,-73.2c19.2,-22.9 40,-43.7 61.9,-64c10.4,-9.7 22.6,-17.7 33.8,-26.6c9,-7.2 17.7,-14.7 25.9,-22.8c2.3,-0.5 4.2,-2.1 4.6,-4.7c0.6,-0.6 1.2,-1.3 1.8,-1.9c3.8,-4.4 0,-10.2 -5,-10.2zM400.7,201c-10.9,8.7 -22.8,16.5 -33.1,26c-21.8,20.2 -43.4,40.7 -62,63.9c-18.7,23.2 -36.3,46.8 -51.4,72.6c-12.8,21.8 -23.4,45.2 -38.8,65.3c-23.8,-24.2 -45.8,-49.7 -66.9,-76.3c-18.1,-22.7 -37,-45.8 -61.5,-61.6c3.3,-21.8 10.8,-42.6 17.2,-63.6c17.7,10.9 31.2,29.7 43.9,45.4c8.2,10.1 17.3,19.3 25.3,29.6c9.3,12 17.4,24.9 24.6,38.2c2.4,4.4 8.1,2.7 10.3,-0.7c15.3,-23.9 28.4,-49 42,-73.8c13.5,-24.7 28.2,-48.2 44.6,-71.1c27.2,-38 55.8,-79.8 97.4,-103.1c14.8,26.1 15.7,58 30.5,84.1c0,1.5 0.5,3.1 1.5,4.3c0,0.1 0.1,0.2 0.1,0.2c-7.5,7.2 -15.5,14 -23.7,20.6z"
									fill="#000000"
								></path>
							</g>
						</g>
					</svg>
					Clear Completed
				</button>
				<button @click="deleteAllTasks" class="clear__all">Clear All</button>
			</div>
			<todo-task
				@set-completion="setCompletion($event)"
				@delete-task="deleteTask($event)"
				v-for="task in tasks"
				:key="task.id"
				:text="task.text"
				:is-completed="task.isCompleted"
				:id="task.id"
			></todo-task>
		</div>
	</div>
</template>

<style scoped>
*,
*::before,
*::after {
	padding: 0;
	margin: 0;
	border: 0;
	box-sizing: border-box;
}

.container-wr {
	display: flex;
	justify-content: center;
	margin-top: 100px;
}

.container {
	width: 80%;
	max-width: 688px;
	padding: 16px;
	background-color: #ffffff;
	background-color: #aabbcc;
}

.counter {
	display: flex;
	align-items: center;
	margin-bottom: 8px;
}

.counter p {
	font-family: "Nunito", sans-serif;
	font-style: normal;
	font-weight: 400;
	font-size: 48px;
	color: #0a0a0a;
	margin-right: 20px;
	line-height: 1.4;
}

.counter div {
	font-family: "Nunito", sans-serif;
	font-size: 48px;
	font-weight: 400;
	font-style: normal;
	color: #ffffff;
	line-height: 1.4;
	transform: translateY(-4px);
}

.create-task {
	display: flex;
	width: 100%;
	align-items: center;

	margin-bottom: 16px;
}

.create-task input {
	flex-grow: 1;
	padding: 0.5rem;
	height: 2.5rem;

	font-family: "Nunito", sans-serif;
	font-style: normal;
	font-weight: 400;
	font-size: 1rem;
	color: #0a0a0a;

	border: 1px solid #cacaca;
	border-radius: 1px;
	outline: none;
	background-color: #fefefe;
	box-shadow: inset 0 1px 2px hsla(0, 0%, 4%, 0.1);

	transition: all 0.4s ease;
}

.create-task input::placeholder {
	font-family: "Nunito", sans-serif;
	font-style: normal;
	font-weight: 400;
	font-size: 1rem;
	color: #0a0a0a;
	opacity: 0.4;
}

.create-task input:focus,
.create-task input:active {
	border-color: #8a8a8a;
}

.create-task button {
	height: 100%;
	width: 73px;
	padding: 0.85em 1em;

	font-family: "Nunito", sans-serif;
	text-align: center;
	font-size: 0.9rem;
	line-height: 1;
	color: #fefefe;

	border: 1px solid transparent;
	background-color: #2199e8;

	display: block;
	cursor: pointer;

	transition: all 0.2s ease;
}

.create-task button:hover,
.create-task button:focus,
.create-task button:active {
	background-color: #1583cc;
}

.clear {
	display: flex;
	align-items: center;
	justify-content: end;
	height: 41px;

	margin-bottom: 16px;
}

.clear__completed {
	margin-right: 2px;

	display: flex;
	align-items: center;
	justify-content: center;

	height: 100%;
	width: 165px;
	padding: 0.85em 1em;

	font-family: "Nunito", sans-serif;
	text-align: center;
	font-size: 0.9rem;
	line-height: 1;
	color: #fefefe;

	border: 1px solid transparent;
	background-color: #ffae00;

	cursor: pointer;

	transition: all 0.2s ease;
}

.clear__completed:hover,
.clear__completed:focus,
.clear__completed:active {
	background-color: #cc8b00;
}

.clear__completed svg {
	width: 20px;
	height: 20px;
	display: block;
	margin-right: 2px;
}

.clear__all {
	height: 100%;
	width: 102px;
	padding: 0.85em 1em;

	font-family: "Nunito", sans-serif;
	text-align: center;
	font-size: 0.9rem;
	line-height: 1;
	color: #fefefe;

	border: 1px solid transparent;
	background-color: #ec5840;

	cursor: pointer;

	transition: all 0.2s ease;
}

.clear__all:hover,
.clear__all:focus,
.clear__all:active {
	background-color: #da3116;
}
</style>
