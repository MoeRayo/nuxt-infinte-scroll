/* eslint-disable new-cap */
<template>
  <div class="pv4 ph3 bg-washed-yellow h-100 mv3 mh2 br2">
    <div class="flex flex-wrap justify-between-l justify-center">
      <a v-for="image in imageList" :key="image.id" class="w-100 w-40-m w-30-l db center tc black link dim ma2" href="#">
        <img class="db center ba b--black-10 ma2" :src="image.urls.small" :alt="image.alt_description" >
        <dl class="mt2 f6 lh-copy">
          <dt class="clip">Artist</dt>
          <dd class="ml0 gray">{{image.user.name}}</dd>
        </dl>
      </a>
      <Observer @intersect="intersected"/>
    </div>
  </div>
</template>

<script>
import axios from "axios"
import Observer from "@/components/Observer";

export default {
  components: {
    Observer
  },
  data: () => ({
    imageList: [],
    page: 1
  }),
  methods: {
    intersected() {
      axios
        .get(
          `https://api.unsplash.com/photos?page=${this.page}&per_page=10&w=1280&h=1280`,
          {
            headers: {
              Authorization:
                "Client-ID {add your client-ID here}",
              "Accept-Version": "v1"
            }
          }
        )
        .then(response => {
          this.page++;
          const lists = response.data;
          this.imageList = [...this.imageList, ...lists];
        })
        .catch(() => {
          this.imageList = [];
      });
    }
  }
}
</script>