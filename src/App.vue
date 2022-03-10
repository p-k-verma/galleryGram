<template>
  <div id="app">
    <div class="full_data" v-for="(deatils,index) in product_details" :key="index">
      <h1>{{deatils.user.bio}}</h1>
      <img :src="`${deatils.links.download}`" alt="" srcset="" class="img_details">
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
    let a = [1,2,3,4,5,6]
    console.log('an array',a)
    console.log('an destructed array',...a);
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
        console.log(this.product_details,"product details");
      })
      .catch((error) => {
        console.log(error);
      })
    },
    infinite_load(){
      if (window.innerHeight + window.scrollY >= document.body.scrollHeight) {
        console.log("hiiiii");
        this.page++;
        this.apicall();
      }
    }
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
