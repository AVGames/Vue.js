<template>
		<li>
				<img v-bind:src="artist.image[2]['#text']"> 
			<h3> 
				<a v-bind:href="artist.url" target="_blank">{{artist.name}}</a>
			</h3>
		</li>
</template>
<script type="text/javascript">
	export default {
		name:'artist',
		props: ['artist']

	};
</script>

<style scoped >

li{
	margin: 10px;
}

</style>