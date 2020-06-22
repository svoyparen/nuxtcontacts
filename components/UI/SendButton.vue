<template>
	<button
		class="button"
		:class="btnStyle"
		v-bind="#attrs"
		v-on="$listeners">
		<slot />
	</button>
</template>