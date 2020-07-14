<template>
	<div class="input-form">
		<label v-if="label !== null">
			{{ htmlLabel }}
		</label>
		<input
			v-if="type === 'field'"
			type="text"
			:placeholder="htmlPlaceholder"
			v-model.trim="realValue"
		>
		<input
			v-else-if="type === 'email'"
			type="email"
			:placeholder="htmlPlaceholder"
			v-model.trim="realValue"
		>
		<input
			v-else-if="type === 'tel'"
			type="tel"
			:pattern="pattern"
			:placeholder="htmlPlaceholder"
			v-model.trim="realValue"
		>
		<textarea
			v-else-if="type === 'text'"
			:placeholder="htmlPlaceholder"
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
			pattern: { type: String, default: null },
			required: { type: Boolean, default: false },
			count: { type: Number, default: 255 },
			count_textarea: { type: Number, default: 2048 },
			phoneLenght: { type: Number, default: 255 },
		},

		data: () => ({
			realValue: null,
			isValid: true,
		}),

		computed: {
			htmlLabel() {
				if ( this.required ) {
					return `* ${this.label}`
				}

				return this.label
			},
		

			htmlPlaceholder() {
				if ( this.required ) {
					return `* ${this.placeholder}`
				}

				return this.placeholder
			},

		},

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
		},

		methods: {
			validation() {
				if( this.type === 'tel' ) {
					this.isValid =  this.realValue.length === 0 || this.realValue.length === 11
				}
				else if ( this.type === 'email' ) {
					this.isValid = (this.realValue.length > 0) && (this.realValue.length < this.count)
				}
				else if ( this.type === 'text' ) {
					this.isValid = (this.realValue && this.realValue.length < this.count_textarea)
				}
				else {
					this.isValid = this.realValue.length === 0 || (this.realValue.length > 4 && this.realValue.length < this.count)
					//console.log("field " + this.value)

				}
				return this.isValid
			},
		},
	}

</script>

<style>
	
</style>
