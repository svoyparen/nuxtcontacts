<template>
	<div>
		<DropList
			label=""
			placeholder=""
			value=""
			options=""
			disabled
			required
		/>
	</div>	
</template>

<script>
	import DropList from '~/components/DropList'
	export default {
		components: {
			DropList,
		},
/*
		data: () => {
			label:'Title',
			placeholder:'Something here',
			value:2,
			options:{
			},
		}
*/
	}	
</script>
