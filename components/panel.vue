<template>
	<div class="top_panel">
		<span class="add_post" @click="addPost">Добавить статью</span>
		<Popup
			ref="popup"
		/>
	</div>
</template>

<script>
	import Popup from '~/components/popup'

	export default {
		components: {
			Popup,
		},

		methods: {
			addPost() {
				this.$refs.popup.setVisible(true)
			},
		},

	}
</script>

<style>
	.top_panel {
		background-color: #111111;
		color: #f0f0f0;
		position: sticky;
		padding: 15px;
	}
	.add_post {
		border: 2px solid #f0f0f0;
		border-radius: 3px;
		background-color: #77bb00;
		margin: 5px;
		padding: 3px 5px;
		color: #f0f0f0;
	}
</style>