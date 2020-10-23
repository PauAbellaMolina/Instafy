<template>
  <div>
    <!-- <h1>Fetch some data!</h1>
    <button class="w-25" v-on:click="fetch">Fetch Data!</button> -->
    <div v-if="this.page && this.fetchedArtists" class="col-md-12 p-0 d-flex justify-content-center">
      <div id="app" class="p-0 w-100 d-flex justify-content-center"><feed-component @changeView="changeView" v-bind:page="page" v-bind:data="dataArtists"></feed-component></div>
    </div>

    <div v-if="!this.page && this.fetchedSongs" class="col-md-12 p-0 d-flex justify-content-center">
      <div id="app" class="p-0 w-100 d-flex justify-content-center"><feed-component @changeView="changeView" v-bind:page="page" v-bind:data="dataSongs"></feed-component></div>
    </div>
  </div>
</template>

<script>
  import FeedComponent from '../components/FeedComponent';

  export default {
    name: "Main",
    components: {
      FeedComponent,
    },
    data() {
      return {
        access_token: "",
        dataArtists: [],
        dataSongs: [],
        fetchedArtists: false,
        fetchedSongs: false,
        page: true /* If true, show artists, if false, show songs */
      }
    },
    beforeMount() {
      this.getAccessToken();
    },
    methods: {
      changeView() {
        this.page = !this.page;
      },
      getAccessToken() {
        const queryString = window.location.hash;
        let access_token = queryString.substr(0, queryString.indexOf('&token_type=')).substr(queryString.indexOf('=')+1);

        this.access_token = access_token;

        this.fetch();
      },
      async fetch() {
        const headers = { "Authorization": "Bearer "+this.access_token }
        /* fetching artists */
        const resArtists = await fetch(`https://api.spotify.com/v1/me/top/artists?time_range=short_term&limit=21`, { headers });
        const dataArtists = await resArtists.json();
        this.dataArtists = dataArtists;
        this.fetchedArtists = true;
        /* fetching songs */
        const resSongs = await fetch(`https://api.spotify.com/v1/me/top/tracks?time_range=short_term&limit=21`, { headers });
        const dataSongs = await resSongs.json();
        this.dataSongs = dataSongs;
        this.fetchedSongs = true;
      }
    }
  }
</script>
