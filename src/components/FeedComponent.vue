<template>
  <div id="main" class="text-secondary">
    <div id="nav" class="d-flex justify-content-center">
      <span class="p-2">Username</span>
    </div>
    <div id="header" class="d-flex flex-column">
      <div class="d-flex flex-row">
        <img class="imgProfile" src="https://scontent-mad1-1.cdninstagram.com/v/t51.2885-19/s150x150/50082648_367922890430364_8512012525062062080_n.jpg?_nc_ht=scontent-mad1-1.cdninstagram.com&_nc_ohc=cptOnGolE8QAX9eoLXS&oh=b126d22924af25208453116ab4ef8123&oe=5FB9929A" />
        <div class="ml-4 d-flex flex-column w-100">
          <div class="d-flex flex-column">
            <div class="d-flex flex-row justify-content-around">
              <span>10</span>
              <span>10</span>
              <span>10</span>
            </div>
            <div class="d-flex flex-row justify-content-around">
              <span>posts</span>
              <span>fwers</span>
              <span>fwing</span>
            </div>
          </div>
          <div class="w-100 followButton mt-2 d-flex justify-content-center">
            <span class="w-75 p-1 d-flex justify-content-center">Follow</span>
          </div>
        </div>
      </div>
      <div class="w-50 pt-1 ml-2 d-flex flex-column align-content-between">
        <span><strong>Instafy</strong></span>
        <span>Your Spotify top songs as an Insta feed</span>
        <a href="www.pauabella.dev">pauabella.dev</a>
      </div>
    </div>
    <div id="underNav" class="p-2 d-flex justify-content-around">
      <span v-on:click="changeView">Artists</span>
      <span v-on:click="changeView">Songs</span>
    </div>
    
    <div class="d-flex flex-row flex-wrap">
      <div id="body" v-for="item in this.data.items" :key="item.id">
        <div v-if="this.page">
          <img id="children" :src="item.images[1].url" />
        </div>
        <div v-if="!this.page">
          <img id="children" :src="item.album.images[1].url" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      data: Object,
      page: Boolean
    },
    methods: {
      changeView() {
        this.$emit('changeView');
      }
    }
  }
</script>
