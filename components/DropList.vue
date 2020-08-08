<template>
	<div class="drop-list">
		<form>
			<select>
				<option></option>
			</select>
		</form>

	</div>
</template>

<script>
	export default {
		props: {
			label: { type: String },
			placeholder: { type: String },
			value: { type: String, default: null },
			options: { type: Array, default: null },
			disabled: { type: Boolean, default: false },
			required: { type: Boolean, default: false },
		}
	}
	
</script>

<style scoped>
	
</style>
