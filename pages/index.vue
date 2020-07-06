<template>
	<div id="contacts_block">
		<div class="form">
			<h1>Написать письмо</h1>
				<form id="post_form" @submit.prevent="submitForm">
					<fieldset v-bind:disabled=ifFormSend>
						<span class="send_message" v-if="send">Письмо успешно отправлено!</span>
						<div class="input-form">
							<input type="text" placeholder="* Email" v-model.trim="email">
							<span class="helper-text invalid" v-if="!$v.email.required">Поле email не должно быть пустым</span>
							<span class="helper-text invalid" v-if="!$v.email.email">Введите корректный email</span>
						</div>
						<div class="input-form">
							<input type="text" placeholder="* Имя" v-model.trim="firstName">
							<span class="helper-text invalid" v-if="!$v.firstName.required">Поле Имя не должно быть пустым</span>
							<span class="helper-text invalid" v-if="!$v.firstName.minLength">Поле Имя не должно быть меньше 3-х знаков</span>
						</div>
						<div class="input-form">
							<input type="text" placeholder="Отчество" v-model.trim="middleName">
							<span class="helper-text invalid" v-if="!$v.middleName.maxLength">Поле Отчество не должно быть более 255-ти символов</span>
						</div>
						<div class="input-form">
							<input type="text" placeholder="Фамилия" v-model.trim="lastName">
							<span class="helper-text invalid" v-if="!$v.lastName.maxLength">Поле Фамилия не должно быть более 255-ти символов</span>
						</div>
						<div class="input-form">
							<input type="text" placeholder="Телефон" v-model.trim="phoneNumber">
							<span class="helper-text invalid" v-if="!$v.phoneNumber.minLength">Поле Телефон не должно быть меньше 11-ти цифр</span>
							<span class="helper-text invalid" v-if="!$v.phoneNumber.maxLength">Поле Телефон не должно быть больше 11-ти цифр</span>
						</div>

						<div class="input-form">
							<input type="text" placeholder="* Тема" v-model.trim="title">
							<span class="helper-text invalid" v-if="!$v.title.required">Поле Тема не должно быть пустым</span>
						</div>
						<div class="input-form">
							<textarea name="text" placeholder="* Текст письма" v-model="text"></textarea>
							<span class="helper-text invalid" v-if="!$v.text.required">Поле Текст не должно быть пустым</span>
							<span class="helper-text invalid" v-if="!$v.text.maxLength">Поле Текст не должно содержать более 2048 символов</span>
						</div>
						<div class="input-form">
							<button type="submit">Отправить</button>

						</div>
						<div class="message">Поля, отмеченные *, обязательны к заполнению.</div>
					</fieldset>
				</form>
		</div>
		
		<div id="contacts">
			<p>
				<strong>Адрес:</strong> перекресток Кибернетиков и Солдата Воскобойникова, 77а, оф.20<br />
				<strong>Телефоны:</strong> 8-9999-322223<br />
				8-0955-223322<br />
				8-999-8888888<br />
				<strong>Email: </strong>email@pisem.net<br />
			</p>
		</div>
  </div>
</template>

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

<script>
	import axios from "axios"
	import Vue from 'vue'
	import Vuelidate from 'vuelidate'
	Vue.use(Vuelidate)
	import { required, minLength, maxLength, email, text, number, string } from "vuelidate/lib/validators"

	//const regex_email = '/^[a-zA-Z0-9._-&]+@([a-zA-Z0-9._-&]++.[a-zA-Z]2-5)+$/'
	//const regex_phone = '/^(\d)11$/'
	export default {
		data: () => ({
			submitStatus: null,
			send: false,
			ifFormSend: false,
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
					this.ifFormSend = true
					let {email, firstName, lastName, middleName, title, text, phoneNumber} = this
					let response = await axios.post('https://test.cornapi.ru/feedback', {email, firstName, lastName, middleName, title, text, phoneNumber
					}).catch( error => {
						//alert('error ' + error)
						this.ifFormSend = false
						return false
					})
					if (this.ifFormSend != false) {
						console.log(response)
						this.email = ''
						this.firstName = ''
						this.lastName = ''
						this.middleName = ''
						this.title = ''
						this.text = ''
						this.phoneNumber = ''
						this.send = true
						this.ifFormSend = false
					}
				}
		}
	}

</script>
