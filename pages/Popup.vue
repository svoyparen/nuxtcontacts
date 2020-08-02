<template>
	<div>
		<PopupWindow
			title="Заголовок модального окна"
			message="Простое текстовое сообщение"
			okTitle="Закрыть"
		>
		</PopupWindow>

	</div>
</template>

<script>
	import PopupWindow from '~/components/PopupWindow'

	export default {
		components: {
			PopupWindow,
		},

	}
</script>

<style>
	button {
		margin-top: 20px;
		color: #fff;
		font-weight: bold;
		text-transform: uppercase;
		border: none;
		background: #0fc3f5;
		transition: .3s;
	}
</style>