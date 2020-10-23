<template>
  <div class="w-100">
    <div id="underNav" class="p-2 w-100 d-flex justify-content-around">
      <span v-on:click="getArtists">Artists</span>
      <span v-on:click="getTracks">Songs</span>
    </div>
    
    <div class="d-flex flex-row flex-wrap">
      <div id="body" v-for="item in this.data.items" :key="item.id">
        <div v-if="isTrue()">
          <img id="children" :src="item.images[0].url" />
        </div>
        <div v-if="!isTrue()">
          <img id="children" :src="item.album.images[0].url" />
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
      getArtists() {
        this.$emit('getArtists');
      },
      getTracks() {
        this.$emit('getTracks');
      },
      isTrue() {
        if(this.page) {
          return true;
        } else {
          return false;
        }
      }
    }
  }
</script>
