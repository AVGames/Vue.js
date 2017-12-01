<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1> PlatziMusic</h1>
      <select v-model="selectedCountry" >
        <option  v-for="country in countries" v-bin:value="country.value"> {{country.name}}</option>
      </select>
      <spinner v-show="loading" ></spinner>
    <ul>
      <artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid" ></artist>
    </ul>
    </div>
</template>

<script>
import spinner from './components/spinner.vue'
import getArtists from './api/index.js'
import artist from './components/artist.vue'
export default {
  name: 'app',
  data () {
    return {
      artists:[],
      countries: [
      { name: 'Venezuela', value: 'Venezuela'},
      { name: 'Argentina', value: 'argetina'},
      { name: 'Colombia', value: 'colombia'},
      ],
      selectedCountry: 'Venezuela',
      loading: true
    }
  },
  components: {
    artist,
    spinner
  },
  methods:{
    refreshArtirst(){
      const _this = this
      this.loading = true;
      this.artists = []
      getArtists(this.selectedCountry)
        .then(function(artists){
          _this.loading = false;
          _this.artists = artists
      })
    }, 
  },
  mounted(){
    this.refreshArtirst()      
  },
  watch: {
    selectedCountry() {
      this.refreshArtirst()
    }
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
