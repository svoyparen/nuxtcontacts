<template>
	<div id="contacts_block">
		<div class="form">
			<h3>Написать письмо</h3>
				<form id="post_form" @submit.prevent="submitForm">
					<fieldset :disabled=isFormSend>
						<span class="send_message" v-if="send">Письмо успешно отправлено!</span>
						<FormInput
							type="email"
							placeholder="Email"
							v-model="email"
							ref="email"
							required
							message = "Wrong email"
						/>
						<FormInput
							type="tel"
							placeholder="Телефон"
							v-model="phoneNumber"
							ref="phoneNumber"
							message = "Wrong phone number"
						/>
						<FormInput
							placeholder="Имя"
							v-model="firstName"
							ref="firstName"
							required
							message = "Wrong first name"
							class="fio"
						/>
						<FormInput
							placeholder="Отчество"
							v-model="middleName"
							ref="middleName"
							message = "Wrong middle name"
							class="fio"
						/>
						<FormInput
							placeholder="Фамилия"
							v-model="lastName"
							ref="lastName"
							message = "Wrong last name"
							class="fio"
						/>
						<FormInput
							placeholder="Тема"
							v-model="title"
							ref="title"
							required
							message = "Wrong title"
							class="theme"
						/>
						<FormInput
							type="text"
							placeholder="Текст письма"
							v-model="text"
							ref="text"
							message = "Wrong text size"
							required
							class="textarea"
						/>
						<div class="input-form">
							<button type="submit">Отправить</button>
						</div>
					</fieldset>
				</form>
		</div>
	</div>
</template>

<script>
	import axios from "axios"
	import FormInput from '~/components/FormInput'

	export default {
		components: {
			FormInput,
		},

		data: () => ({
			submitStatus: null,
			send: false,
			isFormSend: false,
			email: '',
			firstName: '',
			lastName: '',
			middleName: '',
			title: '',
			text: '',
			phoneNumber: '',
			errors: [],
		}),
		methods: {
			async submitForm(event){
				this.isFormSend = true
				this.errors = []

				if(!this.$refs.email.validation()){
					this.errors.push('Введен некорректный email')
				}
				if(!this.$refs.firstName.validation()){
					this.errors.push('Не указано Имя')
				}
				if(!this.$refs.middleName.validation()){
					this.errors.push('Указано некорректное значение в поле Отчество')
				}
				if(!this.$refs.lastName.validation()){
					this.errors.push('Указано некорректное значение в поле Фамилия')
				}
				if(!this.$refs.phoneNumber.validation()){
					this.errors.push('Введен некорректный номер телефона')
				}
				if(!this.$refs.title.validation()){
					this.errors.push('Не указана тема письма')
				}
				if(!this.$refs.text.validation()){
					this.errors.push('Введено некорректное значение в поле Текст')
				}
				if(this.errors.length > 0) {
					console.log('There are some errors:\n' + this.errors)
					this.isFormSend = false
					return false
				}

				let {email, firstName, lastName, middleName, title, text, phoneNumber} = this

				let response = await axios.post('https://test.cornapi.ru/feedback', {email, firstName, lastName, middleName, title, text, phoneNumber
				}).catch( error => {
					console.log( error )
					this.isFormSend = false
					return false
				})

				if (this.isFormSend !== false) {
					console.log(response)
					this.email = ''
					this.firstName = ''
					this.lastName = ''
					this.middleName = ''
					this.title = ''
					this.text = ''
					this.phoneNumber = ''
					this.send = true
					this.isFormSend = false
				}
			}
		}
	}

</script>

<style>
	#post_form label {
		text-align: center;
		font-size: 14px;
		color: white;
	}
	#post_form .message {
		text-align: center;
		font-size: 12px;
		color: white;
	}
	.invalid {
		margin:15px 40px;
		padding: 5px;
		font-size: 14px;
		background-color: #fff;
		color: red;
	}
	.send_message {
		margin:15px 40px;
		font-size: 14px;
		padding: 5px;
		background-color: #fff;
		color:green;
	}
	fieldset {
		border:0px;
	}
</style>