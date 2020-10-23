<template>
  <div id="header" class="p-0">
    <div id="nav" class="d-flex justify-content-start">
      <span class="pt-2 pl-2 pb-1 ml-1"><strong>{{this.data['user']['username']}}</strong></span>
    </div>
    <div id="header" class="d-flex flex-column">
      <div class="d-flex flex-row">
        <img class="imgProfile" :src="this.data['user']['profile_pic_url']" /> <!-- We can also use the hd profile img but it's not worth from the performance prespective -->
        <div class="ml-4 d-flex flex-column w-100">
          <div class="userInfoCounters d-flex flex-column">
            <div class="d-flex flex-row justify-content-around">
              <div class="d-flex flex-column align-items-center">
                <span>{{this.data['user']['edge_owner_to_timeline_media']['count']}}</span>
                <span class="label">posts</span>
              </div>
              <div class="d-flex flex-column align-items-center">
                <span>{{this.data['user']['edge_followed_by']['count']}}</span>
                <span class="label">followers</span>
              </div>
              <div class="d-flex flex-column align-items-center">
                <span>{{this.data['user']['edge_follow']['count']}}</span>
                <span class="label">following</span>
              </div>
            </div>
          </div>
          <div class="w-100 followButton mt-2 d-flex justify-content-center">
            <span class="w-75 p-1 d-flex justify-content-center">Follow</span>
          </div>
        </div>
      </div>
      <div class="w-75 pt-2 ml-2 d-flex flex-column align-content-between">
        <span><strong>{{this.data['user']['full_name']}}</strong></span>
        <!-- DECIDE IF WE SHOULD SHOW THE USERS BIO OR OUR TEXT HMM -->
        <!-- <span>{{this.data['user']['biography']}}</span> -->
        <span>Cool right?</span>
        <span>Come get your Instafy Feed here:</span>
        <a href="https://instafy.me">instafy.me</a>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      data: Object,
    },
  } 
</script>