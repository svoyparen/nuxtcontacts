<template>
	<div id="contacts_block">
		<div class="form">
			<h1>Написать письмо</h1>
				<form id="post_form" @submit.prevent="submitForm">
					<fieldset :disabled=isFormSend>
						<span class="send_message" v-if="send">Письмо успешно отправлено!</span>
						<span class="invalid" v-else>Не заполнены необходимые поля!</span>
						<FormInput
							type="email"
							placeholder="Email"
							v-model="email"
							required
						/>
						<FormInput
							placeholder="Имя"
							v-model="firstName"
							required
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
							type="tel"
							placeholder="Телефон"
							v-model="phoneNumber"
							pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
						/>
						<FormInput
							placeholder="Тема"
							v-model="title"
							required
						/>
						<FormInput
							type="text"
							placeholder="Текст письма"
							v-model="text"
							required
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
			
		}),
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