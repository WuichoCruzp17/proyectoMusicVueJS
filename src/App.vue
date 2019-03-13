<template lang="pug">
#app
   section.section
     nav.nav.has-shadow
      .container
        input.input.is-large(type="text", placeholder="Buscar canciones" v-model='searchQuery')
        a.button.is-info.is-large(@click="search") Buscar
        a.button.is-danger.is-large &times;
        p {{searchMessage}}
     .container.results
      .columns
        .column(v-for="t in tracks") {{t.name}} - {{t.artist}}

</template>

<script>
import trackService from './services/track'
export default {
  name: 'app',
  data () {
    return {
      searchQuery: '',
      tracks: []
    }
  },
  computed: {
    searchMessage () {
      return `Encontrados: ${this.tracks.length}`
    }
  },
  watch: {
    name (newVal, oldVal) {
      console.log(newVal, oldVal)
    }
  },
  methods: {
    search () {
      trackService.search(this.searchQuery)
        .then(function (res) {
          console.log(res)
        })
    }
  }
}
</script>

<style lang="scss">
@import './scss/main.scss';

.results {
  margin-top:50px;
}
</style>
