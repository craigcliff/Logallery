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
    :style="{ backgroundImage: 'url(' + person + ')', width: '450px', height: '450px' ,backgroundSize: 'cover'}"
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
        InitialImages: 0
      };
    },
  components: {
    
  },
  methods: {
  getInitialUsers () {
      if (parseInt(this.getW) > 400){
          this.InitialImages = 30
      }
      else{
this.InitialImages = 5
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
        console.log("The width is: " + this.getW )
    }
  
},

mounted() {
 this.scroll(this.person);
 this.getWidth()
},

beforeMount() {
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
  width: 200px; 
  margin: .5vw; 

    }

    


    @media screen and (max-width: 400px) {
  .cards .image { margin: 0; }
  .cards { padding: 0; }
  
}
    


  
</style>