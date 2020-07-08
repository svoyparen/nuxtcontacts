<template>
	<div id="contacts_block">
		<div class="form">
			<h1>Написать письмо</h1>
				<form id="post_form" @submit.prevent="submitForm">
					<fieldset v-bind:disabled=isFormSend>
						<span class="send_message" v-if="send">Письмо успешно отправлено!</span>
						<FormInput
							placeholder="Email"
							v-model="email"
						/>
						<FormInput
							placeholder="Имя"
							v-model="firstName"
						/>
						<FormInput
							placeholder="Отчество"
							v-model="middleName"
						/>
						<FormInput
							placeholder="Фамилия"
							v-model="lastName"
						/>
						<FormInput
							placeholder="Телефон"
							v-model="phoneNumber"
						/>
						<FormInput
							placeholder="Тема"
							v-model="title"
						/>
						<FormInput
							type="text"
							placeholder="Текст письма"
							v-model="text"
						/>
						<div class="input-form">
							<button type="submit">Отправить</button>

						</div>
					</fieldset>
				</form>
		</div>
		
<!--
		<div id="contacts">
			<p>
				<strong>Адрес:</strong> перекресток Кибернетиков и Солдата Воскобойникова, 77а, оф.20<br />
				<strong>Телефоны:</strong> 8-9999-322223<br />
				8-0955-223322<br />
				8-999-8888888<br />
				<strong>Email: </strong>email@pisem.net<br />
			</p>
		</div>
-->
	</div>
</template>

<script>
	import axios from "axios"
	import Validate from 'vee-validate'
	import { required, minLength, maxLength, email, text, number, string } from "vuelidate/lib/validators"
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
			
		}),

		validations: {
			email: {email, required, minLength:minLength(8),maxLength: maxLength(255)},
			title: {string, required, minLength:minLength(4),maxLength: maxLength(255)},
			firstName: {string, required, minLength:minLength(3),maxLength: maxLength(255)},
			text: {required, minLength:minLength(50), maxLength: maxLength(2048), text},
			lastName: {maxLength: maxLength(255), string},
			middleName: {maxLength: maxLength(255), string},
			// правило не работает. не нашел пока нужное свойство для точного указания количества и в цифрах. Может регулярным выражением?
			phoneNumber: { minLength: minLength(11), maxLength: maxLength(11), number},
		},

		methods: {
			async submitForm(event){
					this.isFormSend = true
					
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
		background-color: #fff;
		color: red;
	}
	.send_message {
		margin:15px 40px;
		font-size: 14px;
		background-color: #fff;
		color:green;
	}
	fieldset {
		border:0px;
	}
</style>