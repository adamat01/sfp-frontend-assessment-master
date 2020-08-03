<template>
	<div>
		<div class="grid">
			<movie v-for="movie in movies" :key="movie.id" :title="movie.title" :image="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :rating="movie.vote_average" />
		</div>
		<div class="pagination">
			<!-- 1. Add logic to these pagination links so they appear on the page correctly. -->
			<!-- 2. Add click events that update the page variable. -->
			<!-- [First] [3] [4] [5] [Last] -->
			<a href="#movies"><button v-on:click="page = 1" class="bookend">First</button></a>
			<a href="#movies"><button v-on:click="page -= 4" v-if="page-4>0">{{ page - 4 }}</button></a>
			<a href="#movies"><button v-on:click="page -= 3" v-if="page-3>0">{{ page - 3 }}</button></a>
			<a href="#movies"><button v-on:click="page -= 2" v-if="page-2>0">{{ page - 2 }}</button></a>
			<a href="#movies"><button v-on:click="page -= 1" v-if="page-1>0">{{ page - 1 }}</button></a>
			<a href="#movies"><button class="current">{{ page }}</button></a>
			<a href="#movies"><button v-on:click="page += 1" v-if="page+1<totalPages">{{ page + 1 }}</button></a>
			<a href="#movies"><button v-on:click="page += 2" v-if="page+2<totalPages">{{ page + 2 }}</button></a>
			<a href="#movies"><button v-on:click="page += 3" v-if="page+3<totalPages">{{ page + 3 }}</button></a>
			<a href="#movies"><button v-on:click="page += 4" v-if="page+4<totalPages">{{ page + 4 }}</button></a>
			<a href="#movies"><button v-on:click="page = totalPages" class="bookend">Last</button></a>
		</div>

		<footer class="source">
			<a href="https://www.themoviedb.org/"><img src="https://www.themoviedb.org/assets/2/v4/logos/v2/blue_short-8e7b30f73a4020692ccca9c88bafe5dcb6f8a62a4c6bc55cd9ba82bb2cd95f6c.svg"></a>
		</footer>
	</div>
</template>

<script>
import Movie from './Movie';
import axios from 'axios';
export default {
	components: { Movie },

	props: ['genre'],

	data() {
		return {
			page: 1,
			movies: [],
			totalPages: 500
		}
	},

	// Call the API on startup.
	mounted() {
		this.callAPI();
	},

	// Anytime the genre or page variable is updated, call the API.
	watch: {
		genre() {
			this.page = 1;
			this.callAPI();
		},
		page() {
			this.callAPI();
		}
	},

	methods: {
		callAPI() {
			var ex = '';
			if (this.genre == 28) {
				ex = '27205'
			}else if (this.genre == 16) {
				ex = '330457'
			}else if (this.genre == 80) {
				ex = '475557'
			}else if (this.genre == 18) {
				ex = '244786'
			}else if (this.genre == 14) {
				ex = '671'
			}else if (this.genre == 27) {
				ex = '474350'
			}
			
			axios.get('https://api.themoviedb.org/3/movie/' + ex +
			'/similar?api_key=ec8d397c1839f64ffb1016d7f0621b77&language=en-US&page=' +
			this.page).then((response) => {
				console.log(response.data);
				this.totalPages = response.data.total_pages;
				this.movies = response.data.results
			}, (error) => {
				console.log(error);
			});
		}

		 
			// 1. Make an ajax request to TMDb with the correct page and genre.
			// 2. Update the following variables: movies, totalPages.

			
	}
}
</script>