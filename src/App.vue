<template>
	<div class="container">
		<header>
			<div class="navi">
				<img src="./assets/logo-01.png" alt="Company Logo">
				<nav>
					<table class="bar">
						<tr>
							<td v-for="(genre, index) in genres" @click="currentGenreId = genre.id" :key="index" v-text="genre.name"></td>
						</tr>
					</table>
				</nav>
			</div>
		</header>
		<section class="hero">
			<h1 v-text="currentGenre.name"></h1>
			<a href="#movies"><button type="button">View List</button></a>
		</section>
		<section class="app" id="movies">
			<h2>{{ currentGenre.name }} Movies</h2>
			<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
			<grid :genre="currentGenreId"></grid>
		</section>
	</div>
</template>

<script>
import Grid from './components/Grid';
export default {
	components: {
		Grid
	},
	data() {
		return {
			genres: [
				{ name: 'Action', id: 28 },
				{ name: 'Animation', id: 16 },
				{ name: 'Crime', id: 80 },
				{ name: 'Drama', id: 18 },
				{ name: 'Fantasy', id: 14 },
				{ name: 'Horror', id: 27 },
			],
			currentGenreId: 28
		}
	},
	computed: {
		currentGenre() {
			return this.genres.find(genre => genre.id == this.currentGenreId);
		}
	}
}
</script>