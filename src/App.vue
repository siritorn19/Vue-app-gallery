<template>
  <div id="app">
    <div class="container">
      <div>
        <img src="./assets/download.png" alt="" class="logo">
      </div>
      <div class="button-wrapper">
        <button class="btn" @click="searchUnsplash('Cofee')"><b>Cofee</b></button>
        <button class="btn" @click="searchUnsplash('Tea')"><b>Tea</b></button>
        <button class="btn" @click="searchUnsplash('Office')"><b>Office</b></button>
        <button class="btn" @click="searchUnsplash('Foods')"><b>Foods</b></button>
        <button class="btn" @click="searchUnsplash('Sportcar')"><b>Sportcar</b></button>
        
      </div>
      <stack
              :column-min-width="300"
              :gutter-width="15"
              :gutter-height="15"
              monitor-images-loaded
      >
        <stack-item
                v-for="(image, i) in images"
                :key="i"
                style="transition: transform 300ms"
        >
          <img :src="image.urls.small" :alt="image.alt_description" />
        </stack-item>
      </stack>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { Stack, StackItem } from "vue-stack-grid";

export default {
  name: 'app',
  components: { 
    Stack, 
    StackItem 
},
  data: () => ({ 
    images: [] 
  }),
  methods:{
    searchUnsplash(topic) { 
    this.images = []; 
    axios .get( `https://api.unsplash.com/search/photos?query=${topic}&per_page=30`, 
    { 
        headers: { 
           Authorization: "Client-ID nHmoDP82kBWDQH1dcL2t-Z_ZzA0Fp4gOxVES-BzOpwE", 
           "Accept-Version": "v1" 
        } 
    }) 
    .then(response => { 
        this.images = response.data.results; 
    })
    .catch(() => { 
       this.images = []; 
    }); 
}
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container { 
    width: 80vw; 
    margin: 0 auto; 
} 
.button-wrapper { 
    display: flex; 
    justify-content: center; 
    margin-bottom: 25px; 
    border-radius:10px;
} 
.btn { 
    font-size: 18px; 
    background-color: red; 
    color: #fff; 
    padding: 10px 30px;
    font-weight: 500;
    border:none;
    border-radius:10px;
}
.btn:not(:last-child) { 
    margin-right: 15px; 
     border-radius:10px;
}

img { 
    width: 100%; 
    height: auto; 
    border-radius: 12px; 
}
.logo{
  width: 300px;
}
</style>
