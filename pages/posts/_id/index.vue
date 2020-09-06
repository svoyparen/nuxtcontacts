<template>
	<div>
		<h2>Выбрана статья номер {{ this.id }}</h2>
		<h3 class="title">Title: {{ this.title }}</h3>
		<div class="text">
			{{ this.text }}
		</div>

	</div>
</template>

<script>
	import axios from 'axios'
	export default {


		data: () => ({
			id: '',
			title: '',
			text:'',
			createdAt:'',
			updatedAt:'',
		}),

		//validate(data){
		//	return /^\d+$/.test(data.params.id)
		//},

	    mounted() {
	    	this.id = this.$route.params.id
	    	this.getData()
	    },

	    methods: {
	      getData(args = []) {
	        axios.get('https://test.cornapi.ru/blog')
	        .then( response => {
	        	for ( const item in response.data.data.items ){
					if(response.data.data.items[item]['id'] == this.id) {
						this.title = response.data.data.items[item]['title']
						this.text = response.data.data.items[item]['text']
						this.createdAt = response.data.data.items[item]['createdAt']
						this.updatedAt = response.data.data.items[item]['updatedAt']
						return true
					}
	        	}
	        	this.$router.push('/page404')
	        })
	      },

	  }

	}
</script>

<style>
	.title {
		color: #555;
		font-family: sans-serif;
	}
	.text {
		color: #555;
		font-family: sans-serif;
	}
</style>