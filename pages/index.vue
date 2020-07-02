<template>
	<div id="contacts_block">
		<div class="form">
			<h1>Написать письмо</h1>
				<form id="post_form" @submit.prevent="submitForm">
					<span class="send_message" v-if="send">Письмо успешно отправлено!</span>
					<div class="input-form">
						<label for="email">* Ваш email</label>
						<!--<input type="text" placeholder="Email" v-model.trim="email" :class="{invalid: ($v.email.$dirty && !$v.email.required) || ($v.email.$dirty && !$v.email.email)}">
						<input type="email" placeholder="Email" v-model.trim="email" @blur="isIncorrectEmail">-->
						<input type="email" placeholder="Email" v-model.trim="email">
						<span class="helper-text invalid" v-if="submitted && !$v.email.required">Поле email не должно быть пустым</span>
						<span class="helper-text invalid" v-if="submitted && !$v.email.email">Введите корректный email</span>
						<span class="helper-text invalid" v-if="submitted && !$v.email.minLength">Поле email не должно быть меньше 8-и знаков</span>
					</div>
					<div class="input-form">
						<label for="firstName">* Ваше имя</label>
						<input type="text" placeholder="Имя" v-model.trim="firstName" id="firstName" name="firstName">
						<span class="helper-text invalid" v-if="submitted && !$v.firstName.required">Поле Имя не должно быть пустым</span>
						<span class="helper-text invalid" v-if="submitted && !$v.firstName.minLength">Поле Имя не должно быть меньше 3-х знаков</span>
					</div>
					<div class="input-form">
						<label for="middleName">Отчество</label>
						<input type="text" placeholder="Отчество" v-model.trim="middleName">
						<span class="helper-text invalid" v-if="submitted && !$v.middleName.maxLength">Поле Отчество должно содержать не более 255-ти букв</span>
					</div>
					<div class="input-form">
						<label for="lastName">Фамилия</label>
						<input type="text" placeholder="Фамилия" v-model.trim="lastName">
						<span class="helper-text invalid" v-if="submitted && !$v.lastName.maxLength">Поле Фамилия должно содержать не более 255-ти букв</span>
					</div>
					<div class="input-form">
						<label for="phoneNumber">Телефон</label>
						<input type="text" placeholder="Телефон" v-model.trim="phoneNumber">
						<span class="helper-text invalid" v-if="submitted && !$v.phoneNumber.minLength">Поле Телефон должно содержать не меньше 11-ти цифр</span>
						<span class="helper-text invalid" v-if="submitted && !$v.phoneNumber.maxLength">Поле Телефон должно содержать не больше 11-ти цифр</span>
					</div>
					<div class="input-form">
						<label for="title">* Тема</label>
						<input type="text" placeholder="Тема" v-model.trim="title">
						<span class="helper-text invalid" v-if="submitted && !$v.title.required">Поле Тема не должно быть пустым</span>
						<span class="helper-text invalid" v-if="submitted && !$v.title.maxLength">Поле Тема не должно быть более 255-ти знаков</span>
					</div>
					<div class="input-form">
						<label for="text">* Текст письма</label>
						<textarea name="text" placeholder="Текст письма" v-model="text"></textarea>
						<span class="helper-text invalid" v-if="submitted && !$v.text.required">Поле Текст не должно быть пустым</span>
					</div>
					<div class="input-form">
						<!--<button v-on:click="submitForm" type="submit">Отправить</button>-->
						<button type="submit">Отправить</button>
					</div>
					<div class="message">Поля, отмеченные *, обязательны к заполнению.</div>
					
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
</style>

<script>
	import axios from "axios"
	import Vue from 'vue'
	import Vuelidate from 'vuelidate'
	Vue.use(Vuelidate)
	import { required, minLength, maxLength, email, text, number, string } from "vuelidate/lib/validators"

	//const regex_email = '/^[a-zA-Z0-9а-яА-Я._-&]+@([a-zA-Z0-9а-яА-Я._-&]++.[a-zA-Z | рф]2-4)+$/'
	//const regex_email = '/^[a-zA-Z0-9._-&]+@([a-zA-Z0-9._-&]++.[a-zA-Z]2-5)+$/'
	//const regex_phone = '/^(\d)11$/'
	export default {
		data: () => ({
				email: '',
				firstName: '',
				lastName: '',
				middleName: '',
				title: '',
				text: '',
				phoneNumber: '',
				submitted: false,
				send: false
		}),
		validations: {
			email: {email, required, minLength:minLength(8),maxLength: maxLength(255)},
			title: {string, required, minLength:minLength(4),maxLength: maxLength(255)},
			firstName: {string, required, minLength:minLength(3),maxLength: maxLength(255)},
			lastName: {maxLength: maxLength(255), string},
			middleName: {maxLength: maxLength(255), string},
			text: {required, minLength:minLength(50), maxLength: maxLength(2048), text},
			// правило не работает. не нашел пока нужное свойство для точного указания количества и в цифрах. Может регулярным выражением?
			phoneNumber: { minLength: minLength(11), maxLength: maxLength(11), number},
		},
		methods: {
			submitForm (event) {
				this.submitted = true;
				axios.post('https://test.cornapi.ru/feedback', {
					firstName: this.firstName,
					lastName: this.lastName,
					middleName: this.middleName,
					title: this.title,
					email: this.email,
					text: this.text,
					phoneNumber: this.phoneNumber
				}).then( res => {
					this.send = true
					//alert('Smth res ' + res)
					// TODO очистка формы
					event.target.reset()
					this.email = ''
					this.firstName = ''
					this.lastName = ''
					this.middleName = ''
					this.title = ''
					this.text = ''
					this.phoneNumber = ''
					this.submitted = false
				}).catch( error => {
					this.send = false
				}).finally(() => {
					return
				})
			}
		}
	}


</script>