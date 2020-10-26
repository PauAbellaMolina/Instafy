<template>
  <div class="w-100 h-100">
    <div id="underNav" class="p-2 pb-3 w-100 d-flex justify-content-around">
      <span v-on:click="getArtists" ref="artists" class="">Artists</span>
      <span v-on:click="getTracks" ref="tracks" class="">Songs</span>
    </div>
    
    <div class="d-flex flex-row flex-wrap">
      <div id="body" v-for="item in this.data.items" :key="item.id">
        <div v-if="isTrue()">
          <img id="children" :src="item.images[0].url" v-on:click="showLabel" />
          <p id="childrenLabel" ref="label" class="d-none justify-content-center align-items-center text-center" v-on:click="hideLabel">{{item.name}}</p>
        </div>
        <div v-if="!isTrue()">
          <img id="children" :src="item.album.images[0].url" v-on:click="showLabel" />
          <p id="childrenLabel" ref="label" class="d-none justify-content-center align-items-center text-center" v-on:click="hideLabel">{{item.name}}</p>
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
    mounted() {
      this.$refs.artists.className = "labelActive";
    },
    methods: {
      getArtists() {
        this.$emit('getArtists');
        this.$refs.artists.className = "labelActive";
        this.$refs.tracks.classList.remove("labelActive");
      },
      getTracks() {
        this.$emit('getTracks');
        this.$refs.tracks.className = "labelActive";
        this.$refs.artists.classList.remove("labelActive");
      },
      isTrue() {
        if(this.page) {
          return true;
        } else {
          return false;
        }
      },
      showLabel(event) {
        let p = event.target.nextSibling;

        p.classList.remove("d-none");
      },
      hideLabel(event) {
        let p = event.target;

        p.classList.add("d-none");
      }
    }
  }
</script>
