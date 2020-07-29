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
			:placeholder="htmlPlaceholder"
			v-model.trim="realValue"
		>
		<textarea
			v-else-if="type === 'text'"
			:placeholder="htmlPlaceholder"
			v-model.trim="realValue"
		></textarea>
		<span class="invalid" v-if="this.isValid === false" >{{ message }}</span>
	</div>
</template>

<script>
	export default {
		props: {
			value: null,
			label: { type: String, default: null },
			placeholder: { type: String, default: null },
			type: { type: String, default: 'field' },
			required: { type: Boolean, default: false },
			message: { type: String, default: null },
			count: { type: Number, default: null },
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

			counter() {
				if ( this.type === 'tel' ) {
					this.count = 11
				} else if ( this.type === 'field' || this.type === 'email' ) {
					this.count = 255
				} else if ( this.type === 'text' ) {
					this.count = 2048
				} else {
					this.count = 255
				}
				return this.count
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
					this.isValid =  !this.required || ( this.realValue.length === this.counter )
				}
				else if ( this.type === 'email' ) {
					this.isValid = (this.realValue.length > 0) && (this.realValue.length < this.counter )
				}
				else if ( this.type === 'text' ) {
					this.isValid = !this.required || ( this.realValue.length > 0 && this.realValue.length < this.counter )
				}
				else {
					this.isValid = !this.required || ( this.realValue.length > 0 && this.realValue.length < this.counter )
				}
				return this.isValid
			},

			/*
			validation() {
				if( this.type === 'tel' ) {
					this.isValid =  this.realValue.length === this.counter || ( !this.required && this.realValue.length === 0 )
				}
				else if ( this.type === 'email' ) {
					this.isValid = (this.realValue.length > 0) && (this.realValue.length < this.counter )
				}
				else if ( this.type === 'text' ) {
					this.isValid = this.realValue.length > 0 && this.realValue.length < this.counter
				}
				else {
					this.isValid = ( this.realValue.length > 0 && this.realValue.length < this.counter ) || ( !this.required && this.realValue.length === 0 )
				}
				return this.isValid
			},
			*/
		},
	}

</script>

