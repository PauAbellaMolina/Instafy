<template>
  <div id="header" class="p-0">
    <div id="nav" class="d-flex justify-content-start">
      <span class="pt-2 pl-3 pb-1"><strong>{{this.data['user']['username']}}</strong></span>
    </div>
    <div id="header" class="d-flex flex-column">
      <div class="d-flex flex-row">
        <img class="imgProfile col-md-4" :src="this.data['user']['profile_pic_url']" /> <!-- We can also use the hd profile img but it's not worth from the performance prespective -->
        <div class="w-100 ml-4 d-flex flex-column justify-content-center">
          <div class="userInfoCounters d-flex flex-row justify-content-around">
            <div class="d-flex flex-column align-items-center">
              <span class="data">{{this.data['user']['edge_owner_to_timeline_media']['count']}}</span>
              <span class="label">Posts</span>
            </div>
            <div class="d-flex flex-column align-items-center">
              <span class="data">{{this.data['user']['edge_followed_by']['count']}}</span>
              <span class="label">Followers</span>
            </div>
            <div class="d-flex flex-column align-items-center">
              <span class="data">{{this.data['user']['edge_follow']['count']}}</span>
              <span class="label">Following</span>
            </div>
          </div>
        </div>
      </div>
      <div class="w-75 pt-2 ml-2 d-flex flex-column align-content-between">
        <span><strong>{{this.data['user']['full_name']}}</strong></span>
        <!-- DECIDE IF WE SHOULD SHOW THE USERS BIO OR OUR TEXT HMM -->
        <span class="bio">{{this.data['user']['biography']}}</span>
        <!-- <span>Cool right?</span>
        <span>Come get your Instafy Feed here:</span> -->
        <p class="mt-2 font-weight-bold">Get your feed at <span class="font-weight-normal">➜</span> <a href="https://instafy.me">instafy.me</a></p>
      </div>
      <button class="followButton w-100 d-flex justify-content-center" v-on:click="generateImg">
        <span class="w-75 p-1 d-flex justify-content-center">Download</span>
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      data: Object,
    },
    beforeMount() {
      this.data['user']['edge_followed_by']['count'] = this.formatCounters(this.data['user']['edge_followed_by']['count']);
      this.data['user']['edge_follow']['count'] = this.formatCounters(this.data['user']['edge_follow']['count']);
      console.log(this.data['user'])
    },
    methods: {
      generateImg() {
        this.$emit('generateImg');
      },
      formatCounters(num) {
        if(num > 999 && num < 10000){
          return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,');
        }else if(num > 9999 && num < 1000000){
          return (num/1000).toFixed(0) + 'K';
        }else if(num > 1000000){
          return (num/1000000).toFixed(0) + 'M';
        }else if(num < 1000){
          return num;
        }
      }
    }
  } 
</script>