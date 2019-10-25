<template>

    
    <div class="cards">
    <no-ssr>
    <vue-gallery :images="persons" :index="index" @close="index = null"  ></vue-gallery>
     </no-ssr>
    
    
    <div 
    class="image"
    v-for="(person,imageIndex) in persons"
    :key="imageIndex"
    @click="index = imageIndex"
    :style="{ backgroundImage: 'url(' + person + ')', width, height ,backgroundSize: 'cover'}"
    >
      <!-- <div class="left">
        <img :src="person.message">
      </div> -->
      
    </div>
    </div>
 
</template>

<script>



//import VueGallery from 'Vue-Gallery';

export default {
   data: function () {
      return {
        persons: [],
        index: null,
        busy: false,
        limit: 10,
        getW:"",
        InitialImages: 0,
        width: "250px",
        height: '250px'
      };
    },
  components: {
    
  },
  methods: {
  getInitialUsers () {
      if (this.getW > "400"){
          console.log("Width is....... " + this.getW)
          this.InitialImages = 30
          this.width = "450px"
          this.height = "450px"
      }
      else{
          console.log("Width is....... " + this.getW)
this.InitialImages = 10
this.width = "150px"
          this.height = "150px"
      }

      
    
    for (var i = 0; i < this.InitialImages; i++) {
      this.$axios.$get(`https://dog.ceo/api/breeds/image/random`)
        .then(response => {
          this.persons.push(response.message);
         console.log(response)
          //console.log(response.results)
        });
    }
  },
   scroll (person) {
    window.onscroll = () => {
      let bottomOfWindow = document.documentElement.scrollTop + window.innerHeight === document.documentElement.offsetHeight;

      if (bottomOfWindow) {
          for (var i = 0; i < this.InitialImages; i++) {
        this.$axios.$get(`https://dog.ceo/api/breeds/image/random`)
          .then(response => {
           // this.persons.push(response.results[0]);
           this.persons.push(response.message);
           console.log("Scrolling......")
           console.log("Scrolling2222222222222222222222222222......")
           console.log(response)
          });
      }
      }
    };
  },
   getWidth() {	
        this.getW = screen.width;
        console.log(typeof this.getW);
        console.log("The width is: " + this.getW )
    }
  
},

mounted() {
 this.scroll(this.person);
 
},

beforeMount() {
    this.getWidth()
  this.getInitialUsers();
}

}
</script>

<style lang="scss">
 /* Optional Styles */


   .cards {
    // display: flex;
    // flex-wrap: wrap;
    // align-items: flex-start;
    // flex-direction: row;
    // max-height: 100vh;

    padding: .5vw;
  font-size: 0;
  display: -ms-flexbox;
  -ms-flex-wrap: wrap;
  -ms-flex-direction: column;
  -webkit-flex-flow: row wrap; 
  flex-flow: row wrap; 
  display: -webkit-box;
  display: flex;
  }

    .image {
//  -webkit-box-flex: auto;
  -ms-flex: auto;
  flex: auto; 
  width: 100px; 
  margin: .5vw; 

    }

    


    @media screen and (max-width: 400px) {
  .cards .image { margin: .5vw; }
  .cards { padding: 0; }
  
}
    


  
</style>