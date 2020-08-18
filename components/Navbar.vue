<template>
	<div>
		<nav class="navigation">
			<ul class="nav">
				<li v-for="link in navlinks"><a :href="link.url">{{ link.title }}</a></li>
			</ul>
		</nav>
	</div>
</template>

<script>
	export default {
		props: {
			navlinks: { type: Array }
		}
		
	}
	
</script>

<style scoped>
.navigation {
	background-color: #999999;
	padding: 10px;
	margin-bottom: 25px;
}
ul {
	list-style: none;
	margin: 0;
	padding-left: 0;
	display: flex;
	font-style: sans-serif;
}
li {
	
}
a {
	display: block;
	text-decoration: none;
	margin-right: 15px;
	padding: 3px 15px;
	border: 1px solid white;
}
ul li a:hover {
	background-color: white;
}
</style>
