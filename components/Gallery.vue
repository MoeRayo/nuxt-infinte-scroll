/* eslint-disable new-cap */
<template>
  <div class="pv4 ph3 bg-washed-yellow h-100 mv3 mh2 br2">
    <div class="flex flex-wrap justify-between-l justify-center">
      <a v-for="image in images" :key="image.id" class="w-100 w-40-m w-30-l db center tc black link dim ma2" href="">
        <img class="db center ba b--black-10 ma2" :src="image.urls.small" :alt="image.alt_description" >
        <dl class="mt2 f6 lh-copy">
          <dt class="clip">Artist</dt>
          <dd class="ml0 gray">{{image.user.name}}</dd>
        </dl>
      </a>
    </div>
  </div>
</template>

<script>
import axios from "axios"

export default {
  data: () => ({
    images: []
  }),
  mounted(){
    this.searchUnsplash()
  },
  methods: {
    searchUnsplash() {
      this.images = [];
      axios
        .get(
          `https://api.unsplash.com/photos?per_page=21&w=1280&h=1280`,
          {
            headers: {
              Authorization:
                "Client-ID 2IslnBxGaSAz7MpV89-REHyWsFYvt_Id875LcGpVO1o",
              "Accept-Version": "v1"
            }
          }
        )
        .then(response => {
          this.images = response.data;
        })
        .catch(() => {
          this.images = [];
      });
    }
  }
}
</script>