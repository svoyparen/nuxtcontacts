<template>
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
					<button v-on:click="submitForm" type="submit">Отправить</button>
					<button v-on:click="submitForm" type="submit">Отправить</button>
				</div>

			</form>
	</div>
</template>

<script>
	export default {
		data()  {
		    return {
		    	firstName: '',
		    	title: '',
		    	email: '',
		    	text: '',
	    	}
		}
	}
</script>