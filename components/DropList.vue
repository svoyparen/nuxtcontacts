<template>
	<div class="drop-list">
		<div class="select">
			<p
				class="title"
				@click="isHidden = !isHidden">
					{{ selected }}
			</p>
			<div class="options" v-if="isHidden">
				<p 
					class="option"
					v-for="option in options"
					:value="option.value"
					@click="selectOption(option)">
					{{ option.name }}
				</p>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			label: { type: String },
			placeholder: { type: String },
			value: { type: String, default: null },
			//options: { type: Array, default(){ return [{ name: 'Option 1', value: 1 },{ name: 'опция 2', value: 2 }]} },
			options: { type: Array },
			disabled: { type: Boolean, default: false },
			required: { type: Boolean, default: false },
			selected: { type: String, default: '' },
		},

		data: () => ({
			isHidden: false,
		}),

		methods: {
			selectOption(option) {
				console.log(option)
				this.$emit('select',option)
				this.isHidden = false
			},

			hideDropList(){
				this.isHidden = false
			},

		},

		mounted() {
			document.addEventListener('click',this.hideDropList.bind(this), true)
		},

		beforeDestroy() {
			document.removeEventListener('click', this.hideDropList)
		}


	}
	
</script>

<style scoped>
	.drop-list{
		width: 100%;
		height: 100%;
	}
	.select {
		position: relative;
		width: 200px;
	}
	.select p {
		margin: 0;
		background-color: #cecece
	}
	.title {
		border: 1px solid #aeaeae;
		padding: 3px 10px;
	}
	.option {
		padding: 3px 10px;
	}
	.options {
		border: 1px solid #aeaeae;
		position: absolute;
		top:30px;
		right:0;
		width: 100%;
		background-color: #cecece;
	}
	.options p:hover {
		background-color: #aeaeae;
	}
</style>