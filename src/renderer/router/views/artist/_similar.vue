<template>
<div class="page-container similar">
  <section class="page-section">
    <div class="section-header">
      <h1>Similar to {{ $store.state.artist.name }}</h1>
    </div>
    <div class="section-items-container">
      <sectionitem
      v-for="artist in similar"
      :type="artist.type"
      :key="artist.id"
      :image="artist.images[1].url"
      :title="artist.name"
      :primaryID="artist.id"
      ></sectionitem>
    </div>
  </section>
</div>
</template>
<script>
import spotifyApi from '../../../api/'

export default {
  data() {
    return {
      similar: {}
    }
  },
  created() {
    // fetch the data when the view is created and the data is
    // already being observed
    this.fetchData()
  },
  watch: {
    // call again the method if the route changes
    '$route': 'fetchData'
  },
  methods: {
    fetchData() {
      // Get artists similar to this artist from the api
      spotifyApi.getArtistRelatedArtists(this.$route.params.id)
        .then(response => this.similar = response.artists)
    }
  }
}
</script>
