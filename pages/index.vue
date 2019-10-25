<template>
  

     
    <div>
      <no-ssr>
      <Slide>
      <a id="home" href="#">
        <span>Home</span>
      </a>
    </Slide>
        </no-ssr>
       <no-ssr>
    <vue-gallery :images="images" :index="index" @close="index = null"></vue-gallery>
     </no-ssr>
    <div
    
      class="image"
      v-for="(image, imageIndex) in images"
      :key="imageIndex"
      @click="index = imageIndex"
      :style="{ backgroundImage: 'url(' + image + ')', width: '400px', height: '400px' }"
    ></div>
    </div>
  
    
 
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'
//import VueGallery from 'Vue-Gallery';


export default {
   data: function () {
      return {
        images: [
          'https://dummyimage.com/800/ffffff/000000',
          'https://dummyimage.com/1600/ffffff/000000',
          'https://dummyimage.com/1280/000000/ffffff',
          'https://dummyimage.com/400/000000/ffffff',
          'https://dummyimage.com/1280/000000/ffffff',
          'https://dummyimage.com/400/000000/ffffff'
        ],
        index: null
      };
    },
  components: {
    Logo,
    VuetifyLogo
  }
}
</script>

<style scoped>
  .image {
    float: left;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
    border: 1px solid #ebebeb;
    margin: 5px;
  }
</style> 
