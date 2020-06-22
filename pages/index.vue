<template>
	<div id="contacts_block">
		<div class="form">
			<h1>Написать письмо</h1>
				<form id="post_form" @submit.prevent="submitForm">
					<div class="input-form">
						<input type="email" v-model="email" placeholder="Ваш email" name="email" id="email">
					</div>
					<div class="input-form">
						<input type="text" placeholder="Имя"  v-model="firstName" name="firstName" id="firstName">
					</div>
					<div class="input-form">
						<input type="text" placeholder="Тема"  v-model="title" name="title" id="title">
					</div>
					<div class="input-form">
						<textarea name="text" placeholder="Текст письма"  v-model="text" id="text"></textarea>
					</div>
					<div class="input-form">
						<!--<button v-on:click="submitForm" type="submit">Отправить</button>-->
						<button type="submit">Отправить</button>
					</div>

				</form>
		</div>
		
		<div id="contacts">
			<p>
				<strong>Адрес:</strong> перекресток Кибернетиков и Солдата Воскобойникова, 77а, оф.20<br />
				<strong>Телефоны:</strong> 8-9999-322223<br />
				8-0955-223322<br />
				8-999-8888888<br />
			</p>
		</div>
  </div>
</template>


<script>
	import axios from "axios"
	export default {
		data() {
		    return {
		    	firstName: '',
		    	title: '',
		    	email: '',
		    	text: '',
		    	//errors: []
	    	}
		},
		methods: {
			submitForm(event) {
				console.log(this.firstName + ', ' + this.title + ', ' + this.email + ', ' + this.text)
				axios.post('https://test.cornapi.ru/feedback', {
					'firstName': this.firstName,
					'title':  this.title,
					'email': this.email,
					'text': this.text
				}).then( function(res) {
					console.log(res)
				} ).catch(function(error){
					console.log(error)
				})				
			}
		}
	}


</script>