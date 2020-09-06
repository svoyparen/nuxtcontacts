<template>
	<div id="table">
		<table class="table">
			<thead class="thead">
				<th>Номер статьи</th>
				<th>Заголовок статьи</th>
				<th>Текст статьи</th>
				<th>Дата публикации</th>
				<th>Дата обновления</th>
			</thead>
			<tfoot class="tfoot">
				<td>Всего статей</td>
				<td>{{ items.length }}</td>
			</tfoot>
			<tr v-for="item in items" @click="showPopupToEditPost(item)">
				<td>{{ item.id }}</td>
				<td>{{ item.title }}</td>
				<td>{{ item.text }}</td>
				<td>{{ item.createdAt | toLocaleDateString }}</td>
				<td>{{ item.updatedAt | toLocaleDateString }}</td>
				
			</tr>
		</table>
	</div>
</template>

<script>
	export default {
		props: {
			items: Array, required: true
		},

		filters: {
			toLocaleDateString(date) {
				if( date ) {
					return new Date(date).toDateString()
				}
			},
		},

		methods: {
			showPopupToEditPost(item) {
				this.$emit('showPopup', item)
			},
		}

	}
</script>

<style>
	#table {
		width: 100%;
		background-color: #fff;
		padding: 15px;
	}
	th {
		background-color: #fc0;
		border: none;
	}
	tr {
		background-color: #ffc;
		border: none;
	}
	th, td {
		padding: 10px;
		border-bottom: 1px solid black;
	}
	tr:hover {
		background-color: #ccffcc;
	}
	.table {
		
	}
	.tfoot {
		background-color: #f0c0a0;
		
	}
	.thead {

	}

</style>