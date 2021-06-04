<template>
	<main>
		<div class="todo-app">
			<h1 class="heading-for-new-todos">Предстоящие задачи</h1>
			<div class="new-todos">
				<span class="tell-me" v-if="todos.length == 0"
					>У вас нет предстоящих заданий</span
				>
				<itemOftodods
					class="todo-item"
					v-for="item of todos"
					:key="item.id"
					v-bind:itemTodo="item"
					@thisTodoIsChecked="checkedFunction"
					@changetodo="changetodo"
				/>
			</div>
			<h1 class="heading-for-new-todos">Выполненые задачи</h1>
			<div class="new-todos">
				<checkedTodos
					class="todo-item"
					v-for="checkItem of checkedTodos"
					:key="checkItem.id"
					v-bind:itemTodo="checkItem"
					@thisTodosback="thisTodosback"
				/>
			</div>
			<div
				class="add-todo-form"
				:class="{
					'open-form-option': !openOption,
					'red-border': redBorderOn,
				}"
			>
				<div class="input-coloumn">
					<input
						class="heading-input"
						:class="{ 'red-border': redBorderOn }"
						type="text"
						placeholder="Заглавление"
						v-model="headingadd"
					/>
					<textarea
						class="textarea-inp"
						:class="{ 'open-option': !openOption }"
						placeholder="Описание задачи"
						v-model="descriptadd"
					></textarea>
					<div class="mini-inputs">
						<input
							type="text"
							class="deadline-input"
							:class="{ 'open-option': !openOption }"
							placeholder="Дедлайн"
							v-model="deadline"
						/>
						<select
							class="deadline-input"
							:class="{ 'open-option': !openOption }"
							v-model="priority"
						>
							<option value="hight">hight</option>
							<option selected value="middle">middle</option>
							<option value="low">low</option>
						</select>
					</div>
				</div>
				<button
					class="blue-btns"
					@click="this.openOption = !this.openOption"
				>
					<img src="../public/images/more-horizontal.png" alt="" />
				</button>
				<button class="blue-btns" @click="addfunctinon">+</button>
			</div>
		</div>
		<div class="about-todos">
			<p>
				Доброе утро <span class="name">Далер</span>, у вас
				<span class="todos-length" v-if="todos.length > 0"
					>{{ todos.length }} новые задачи</span
				>
				<span class="todos-length" v-if="todos.length == 0"
					>нет новых задач</span
				><br />
				и
				<span class="checkedTodos-length"
					>{{ checkedTodos.length }} выполненые задачи</span
				>
			</p>
		</div>
		<div
			class="change-modal-first"
			:class="{
				'hidden-change-modal': hiddenChangeModal,
				'change-modal': !hiddenChangeModal,
			}"
		>
			<h3>Изменить задачу</h3>
			<div class="change-inputs">
				<input
					class="change-heafing-inp-first"
					type="text"
					placeholder="Заглавление"
					v-model="changeHeading.text"
				/>
				<textarea
					class="change-heafing-inp"
					placeholder="Описание задачи"
					v-model="changeDex.description"
				></textarea>
				<input
					type="text"
					class="change-heafing-inp"
					placeholder="Дедлайн"
					v-model="changeDeadline.deadline"
				/>
				<select
					class="change-heafing-inp"
					v-model="changePriority.priority"
				>
					<option value="hight">hight</option>
					<option value="middle">middle</option>
					<option value="low">low</option>
				</select>
				<button class="save-btn" @click="saveBtn">Сохранить</button>
				<button class="delete-btn" @click="deleteBtn">Удалить</button>
			</div>
		</div>
	</main>
</template>

<script>
import itemOftodods from './components/addedItemTodo'
import checkedTodos from './components/checkedTodos'

export default {
	data() {
		return {
			openOption: false,
			hiddenChangeModal: false,
			redBorderOn: false,
			youHaveNot: false,
			changeHeading: '',
			changeDex: '',
			changeDeadline: '',
			changePriority: '',
			priority: '',
			headingadd: '',
			descriptadd: '',
			deadline: '',
			todos: [
				{
					id: Math.random(),
					text:
						'Позвонить Илону и заказать место на Марсе уже наконец',
					description: 'отправить заказ Цукербергу',
					time: new Date().toLocaleTimeString(),
					deadline: 12,
					priority: 'low',
				},
			],
			checkedTodos: [
				{
					id: Math.random(),
					text: 'Селать техническое задание',
					description: 'отправить заказ Цукербергу',
					time: new Date().toLocaleTimeString(),
					deadline: 12,
					priority: 'low',
				},
			],
		}
	},
	methods: {
		addfunctinon() {
			if (
				this.headingadd.length ||
				(this.descriptadd.length >= 2 && this.hiddenChangeModal == true)
			) {
				// this.hiddenChangeModal = false
				this.todos.push({
					id: Math.random(),
					text: this.headingadd,
					description: this.descriptadd,
					time: new Date().toLocaleTimeString(),
					deadline: this.deadline,
					priority: this.priority,
				})
				;(this.headingadd = ''),
					(this.descriptadd = ''),
					(this.deadline = '')
			} else {
				this.hiddenChangeModal = false
				this.redBorderOn = true
				setTimeout(() => {
					this.redBorderOn = false
				}, 1000)
			}
		},
		checkedFunction(data) {
			let a = this.todos.filter((item) => item.id == data)[0]
			this.todos.splice(this.todos.indexOf(a), 1)
			this.checkedTodos.push(a)
		},
		thisTodosback(data) {
			let d = this.checkedTodos.filter((item) => item.id == data)[0]
			this.checkedTodos.splice(this.checkedTodos.indexOf(d), 1)
			this.todos.push(d)
		},
		changetodo(data) {
			this.hiddenChangeModal = true

			let b = this.todos.filter((item) => item.id == data)[0]
			this.changeHeading = b
			this.changeDex = b
			this.changeDeadline = b
			this.changePriority = b
		},
		saveBtn() {
			this.hiddenChangeModal = !this.hiddenChangeModal
			this.changeHeading = ''
			this.changeDex = ''
			this.changeDeadline = ''
			this.changePriority = ''
		},
		deleteBtn(data) {
			let c = this.todos.filter((item) => item.id == data)[0]
			this.todos.splice(this.todos.indexOf(c), 1)
			this.hiddenChangeModal = !this.hiddenChangeModal
			this.changeHeading = ''
			this.changeDex = ''
			this.changeDeadline = ''
			this.changePriority = ''
		},
	},
	components: {
		itemOftodods,
		checkedTodos,
	},
}
</script>

<style>
@import '../public/css/style.css';
@import '../public/css/fonts.css';
</style>
