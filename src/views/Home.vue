<template>
  <div id="home" class="d-flex flex-row align-items-center">
    <div class="w-100 ml-2 d-flex flex-column align-items-center">
      <h1 class="title">Instafy</h1>
      <h1 class="subtitle mt-3">Get your feed</h1>
      <button class="w-75 mt-2 subtitle" v-on:click="loginSpotify">NOW</button>
      <p class="mt-3">It's 1 sec, trust me</p>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Home",
    methods: {
      loginSpotify() {
        /* DEV */
        // window.location.href = "https://accounts.spotify.com/authorize?client_id=4cd5b87b8c4f4bc9a737094b8a0fd486&redirect_uri=http://localhost:8080&scope=user-top-read&response_type=token";
        /* PROD */
        window.location.href = "https://accounts.spotify.com/authorize?client_id=4cd5b87b8c4f4bc9a737094b8a0fd486&redirect_uri=https://instafy.me&scope=user-top-read&response_type=token";
      }

    }
  };
</script>
