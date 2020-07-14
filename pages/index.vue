<template>
	<div id="contacts_block">
		<div class="form">
			<h1>Написать письмо</h1>
				<form id="post_form" @submit.prevent="submitForm">
					<fieldset :disabled=isFormSend>
						<span class="send_message" v-if="send">Письмо успешно отправлено!</span>
						<FormInput
							type="email"
							placeholder="Email"
							v-model="email"
							ref="email"
							required
						/>
						<span class="invalid" v-if="wrong_email" v-bind="email">{{ wrong_email }}</span>
						<FormInput
							type="field"
							placeholder="Имя"
							v-model="firstName"
							ref="firstName"
							required
						/>
						<span class="invalid" v-if="wrong_firstName" v-bind="firstName">{{ wrong_firstName }}</span>
						<FormInput
							type="field"
							placeholder="Отчество"
							v-model="middleName"
							ref="middleName"
						/>
						<span class="invalid" v-if="wrong_middleName" v-bind="middleName">{{ wrong_middleName }}</span>
						<FormInput
							type="field"
							placeholder="Фамилия"
							v-model="lastName"
							ref="lastName"
						/>
						<span class="invalid" v-if="wrong_lastName" v-bind="lastName">{{ wrong_lastName }}</span>
						<FormInput
							type="tel"
							placeholder="Телефон"
							v-model="phoneNumber"
							pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
							ref="phoneNumber"
						/>
						<span class="invalid" v-if="wrong_phoneNumber" v-bind="phoneNumber">{{ wrong_phoneNumber }}</span>
						<FormInput
							type="field"
							placeholder="Тема"
							v-model="title"
							ref="title"
							required
						/>
						<span class="invalid" v-if="wrong_title" v-bind="title">{{ wrong_title }}</span>
						<FormInput
							type="text"
							placeholder="Текст письма"
							v-model="text"
							ref="text"
							required
						/>
						<span class="invalid" v-if="wrong_text" v-bind="text">{{ wrong_text }}</span>
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
			wrong_email: '',
			wrong_firstName: '',
			wrong_middleName: '',
			wrong_lastName: '',
			wrong_phoneNumber: '',
			wrong_title: '',
			wrong_text: '',
		}),
		methods: {
			async submitForm(event){
				this.isFormSend = true
				this.errors = []

				if(!this.$refs.email.validation()){
					this.errors.push('Введен некорректный email')
					this.wrong_email = 'Введен некорректный email'
				}
				if(!this.$refs.firstName.validation()){
					this.errors.push('Не указано Имя')
					this.wrong_firstName = 'Не указано Имя'
				}
				if(!this.$refs.middleName.validation()){
					this.errors.push('Указано некорректное значение в поле Отчество')
					this.wrong_middleName = 'Некорректное значение в поле Отчество'
				}
				if(!this.$refs.lastName.validation()){
					this.errors.push('Указано некорректное значение в поле Фамилия')
					this.wrong_lastName = 'Некорректное значение в поле Фамилия'
				}
				if(!this.$refs.phoneNumber.validation()){
					this.errors.push('Введен некорректный номер телефона')
					this.wrong_phoneNumber = 'Введен некорректный номер телефона'
				}
				if(!this.$refs.title.validation()){
					this.errors.push('Не указана тема письма')
					this.wrong_title = 'Не указана тема письма'
				}
				if(!this.$refs.text.validation()){
					this.errors.push('Введено некорректное значение в поле Текст')
					this.wrong_text = 'Введено некорректное значение в поле Текст'
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
					this.wrong_email = ''
					this.wrong_firstName = ''
					this.wrong_middleName = ''
					this.wrong_lastName = ''
					this.wrong_phoneNumber = ''
					this.wrong_title = ''
					this.wrong_text = ''
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