<template>
	<div class="col-md-6">
		<img :src="data.image" style="width:50%" />
		<h4>{{ data.title }}</h4>
		<p>{{ data.price }}</p>
		<p>{{ data.caption }}</p>
	</div>
</template>

<script>
export default {
	name: 'card',
	props: {
		data: Object,
	},
};
</script>

<style></style>
