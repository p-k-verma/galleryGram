<template>
  <div id="app">
    <div class="top">
      <div class="gallery" v-for="(deatils,index) in product_details" :key="index">
          <!-- <div>
            <img src="./assets/heart-solid.svg" alt="" srcset="" class="heart">
          </div> -->
        <img :src="`${deatils.urls.regular}`"  alt="" srcset="" class="gallery_image">
      </div>
      <!-- <div ref="productLoader">
        <img src="@/assets/loader.gif" alt="loader">
      </div> -->
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'App',
  components: {
    
  },
  data() {
    return {
      product_details: [],
      page: '1'
    }
  },
  mounted(){

  }
  ,
  created(){
    this.apicall();
    this.infinite_load();
    window.addEventListener("scroll", this.infinite_load);
  },
  methods: {
    async apicall() {
      await axios
      .get(`https://api.unsplash.com/photos/?page=${this.page}&client_id=K__Jo88ggfNZCK2OZIlCs805vo2wa43IBUfcrP5Kd1U`)
      .then((response) => {
        this.product_details.push(...response.data)
      })
      .catch((error) => {
        console.log(error);
      })
    },
    infinite_load(){
      if (window.innerHeight + window.scrollY >= document.body.scrollHeight -1000) {
        console.log("hiiiii");
        this.page++;
        this.apicall();
      }
    },
  },
}
</script>

<style>
.full_data {
  text-align: center;
}
.img_details {
  width: 100%;
  height: 800px;
}
</style>
