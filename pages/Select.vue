<template>
	<div>
		<p> Выбран пункт {{ selected }}</p>
		<DropList
			label="label"
			placeholder="placeholder"
			value="value"
			:options="options"
			disabled
			required
			@select="optionSelected"
			:selected="selected"
		/>
	</div>
</template>

<script>
	import DropList from '~/components/DropList'
	export default {
		components: {
			DropList,
		},

		data () {
			return {
			label:'Title',
			placeholder:'Something here',
			value:2,
			options: [
				{ name: 'Option 1', value: 1 },
				{ name: 'Option 2', value: 2 },
				{ name: 'Option 3', value: 3 },
				{ name: 'Option 4', value: 4 },
			],
			selected:'Select'
			}
		},

		methods: {
			optionSelected(option) {
				this.selected = option.name
			}
		}

	}	
</script>

