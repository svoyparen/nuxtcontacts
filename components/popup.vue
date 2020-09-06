<template>
	<div class="modal-mask" v-if="this.isVisible">
		<div class="modal-container">
			<form class="form">
				<label for="title">Название статьи</label><br />
				<input type="text" name="title" v-model.trim="title"><br />
				<label for="text">Текст статьи</label><br />
				<textarea name="text" v-model.trim="text">{{ text }}</textarea><br />
				<span class="save" @click="save">Сохранить</span>
				<span class="remove" @click="remove">Удалить</span>
			</form>
		</div>
	</div>
</template>

<script>
	import axios from 'axios'
	export default {
		data: () => ({
			isVisible: false,
			isPostSend: false,
			isPostDelete: false,
			id: '',
			title: '',
			text: '',
		}),

		methods: {
			setVisible(flag) {
				console.log('Flag is ' + flag)
				this.isVisible = flag
			},

			setData(item) {
				this.id = item.id
				this.title = item.title
				this.text = item.text
			},

			async save(event) {
				console.log('save')
				let { id, title, text } = this
				if( !id ) {
					let response = await axios.post('https://test.cornapi.ru/blog', {title, text})
						.catch( error => {
							console.log( 'Ошибка! ' + error )
							this.isPostSend = true
							return false
						})
				} else {
					//const editDate = new Date()
					let response = await axios.put('https://test.cornapi.ru/blog/' + id, {title, text})
						.catch( error => {
							console.log( 'Ошибка! ' + error )
							this.isPostSend = true
							return false
						})
				}
			},

			async remove(event) {
				console.log('начинаем удаление ' + this.id + '-й статьи')
				let response = await axios.delete('https://test.cornapi.ru/blog/' + this.id)
					.then(response => {
						this.setVisible(false)
						console.log('удалено!')
					})
					.catch( error => {
						console.log( 'Ошибка! ' + error )
						this.isPostDelete = true
						return false
					})
			},

		}
	}
</script>

<style scoped>
	.modal-mask {
		position: fixed;
		z-index: 9998;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.7);
		display: table;
		transition: opacity 0.9s ease;
	}
	.modal-container {
		max-width: 600px;
		margin: 50px auto;
		background-color: #fff;
		border-radius: 10px;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
		transition: all 0.3s ease;
		font-family: Helvetica, Arial, sans-serif;
	}
	.form {
		width: 90%;
		padding: 15px;
		margin: 15px;
	}
	label {
		color: #111111;
	}
	input {
		width: 100%;
		margin: 15px;
		padding: 15px;
	}
	textarea {
		width: 100%;
		margin: 15px;
		padding: 15px;

	}
	.save {
		margin: 15px;
		background-color: #00cc00;
		color: white;
		padding: 5px 15px;
	}
	.save:hover {
		background-color: #00aa00;
	}
	.remove {
		margin: 15px;
		background-color: #cc3333;
		color: white;
		padding: 5px 15px;
	}
	.remove:hover {
		background-color: #aa1111;
	}
	.remove:click {
		background-color: #550000;
	}

</style>