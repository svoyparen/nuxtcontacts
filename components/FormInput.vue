<template>
	<div class="input-form">
		<label for="" v-if="label !== null">
			{{ label }}
		</label>
		<input
			v-if="type === 'field'"
			type="text"
			:placeholder="placeholder"
			v-model.trim="realValue"
		>
		<textarea
			v-if="type === 'text'"
			:placeholder="placeholder"
			v-model.trim="realValue"
		></textarea>
	</div>
</template>

<script>
	export default {
		props: {
			value: null,
			label: { type: String, default: null },
			placeholder: { type: String, default: null },
			type: { type: String, default: 'field' },
		},

		data: () => ({
			realValue: null,
		}),

		watch: {
			value(value) {
				this.realValue = value
			},

			realValue(value) {
				this.$emit('input', value)
			},
		},

		beforeMount() {
			this.realValue = this.value
		}
	}

</script>

<style>
	
</style>