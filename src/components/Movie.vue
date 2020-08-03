<template>
	<div class="movie">
		<div class="poster" :style="{ backgroundImage: 'url(' + image + ')' }"></div>
		<p class="title" v-text="title"></p>
		<p class="rating">Average Rating: {{ rating }}</p>
	</div>
</template>

<script>
export default {
	props: ['image', 'rating', 'title']
}
</script>