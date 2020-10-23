<template>
  <div class="d-flex justify-content-center">
    <button class="w-25" v-on:click="loginSpotify">Go!</button>
  </div>
</template>

<script>
  export default {
    name: "Home",
    methods: {
      loginSpotify() {
        window.location.href = "https://accounts.spotify.com/authorize?client_id=4cd5b87b8c4f4bc9a737094b8a0fd486&redirect_uri=http://localhost:8080&scope=user-top-read&response_type=token";
      }

    }
  };
</script>
