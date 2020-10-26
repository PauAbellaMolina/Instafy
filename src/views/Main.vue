<template>
  <div class="d-flex justify-content-center align-items-start h-100">
    <div id="ig" class="d-flex flex-column justify-content-center align-items-center h-100" v-if="!this.fetchedIG">
      <h1 class="title text-center">Your <span class="specialTS">IG</span> username</h1>
      <input @keyup.enter="handleIGUsername" class="pl-3 w-50" v-model="igUsername" type="text" name="igUsername" ref="igUsername" placeholder="Username" />
      <button class="w-50 mt-3" v-on:click="handleIGUsername">Go!</button>
      <p class="mt-3" v-if="fetcheIGError != ''">{{this.fetcheIGError}}</p>
    </div>

    <div v-if="this.fetchedIG" ref="main" id="main">
      <div id="app" v-if="this.fetchedIG">
        <header-component :data="dataIG" @generateImg="generateImg"></header-component>
      </div>
      <div v-if="this.page && this.fetchedArtists" id="photos" class="col-md-12 p-0 d-flex justify-content-center">
        <div id="app" class="p-0 w-100 d-flex justify-content-center"><feed-component @getTracks="getTracks" :page="page" :data="dataArtists"></feed-component></div>
      </div>

      <div v-if="!this.page && this.fetchedSongs" id="photos" class="col-md-12 p-0 d-flex justify-content-center">
        <div id="app" class="p-0 w-100 d-flex justify-content-center"><feed-component @getArtists="getArtists" :page="page" :data="dataSongs"></feed-component></div>
      </div>
    </div>
  </div>
</template>

<script>
  import domtoimage from 'dom-to-image';
  import { saveAs } from 'file-saver';
  saveAs
  
  import FeedComponent from '../components/FeedComponent';
  import HeaderComponent from '../components/HeaderComponent';

  export default {
    name: "Main",
    components: {
      FeedComponent,
      HeaderComponent,
    },
    data() {
      return {
        access_token: "",
        igUsername: "",
        dataArtists: [],
        dataSongs: [],
        dataIG: [],
        fetchedArtists: false,
        fetchedSongs: false,
        fetchedIG: false,
        fetcheIGError: "",
        page: true /* If true, show artists, if false, show tracks */
      }
    },
    beforeMount() {
      this.getAccessToken();
    },
    methods: {
      getArtists() {
        this.page = true;
      },
      getTracks() {
        this.page = false;
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
        console.log(this.dataSongs);
      },
      async handleIGUsername() {
        if(this.igUsername == "") {
          this.fetcheIGError = "Username can't be empty"
        } else {
          const resIG = await fetch(`https://www.instagram.com/` + this.igUsername + `/?__a=1`)
          const dataIG = await resIG.json();
          if(dataIG['graphql'] == undefined) {
            this.fetchedIG = false;
            this.fetcheIGError = "Username not found";
          } else {
            this.dataIG = dataIG['graphql'];
            this.fetchedIG = true;
          }
        }
      },
      generateImg() {
        let node = this.$refs.main;

        domtoimage.toBlob(node)
        .then(function (blob) {
            window.saveAs(blob, 'InstafyFeed.png');
        });
      }
    }
  }
</script>
