<template>
  <div id="app">
    <home v-on:search="search"></home>
    <search-result v-if="results.length > 0" :movies="results" :search-input="searchInput"></search-result>
  </div>
</template>

<script>
import Home from './components/Home'
import SearchResult from './components/SearchResult'

export default {
  name: 'app',
  components: {
    Home,
    SearchResult
  },
  data: function () {
    return {
      searchInput: '',
      results: []
    }
  },
  methods: {
    search: function (input) {
      this.searchInput = input

      // Do search

      this.results = [
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        },
        {
          poster_path: '/5aGhaIHYuQbqlHWvWYqMCnj40y2.jpg',
          overview: 'During a manned mission to Mars, Astronaut Mark Watney is presumed dead after a fierce storm and left behind by his crew. But Watney has survived and finds himself stranded and alone on the hostile planet. With only meager supplies, he must draw upon his ingenuity, wit and spirit to subsist and find a way to signal to Earth that he is alive.',
          release_date: '2015-09-30',
          title: 'The Martian'
        }
      ]
    }
  }
}
</script>

<style src="assets/css/normalize.css"></style>
<style src="assets/css/skeleton.css"></style>
