<template>
  <div id="app">
    <!-- <GetDogImage/> -->
    <!-- <GetCatImage/> -->

    <!-- GetImage는 component요소로 자식요소와 연결해준다. -->
    <!-- btnName은 GetImage의 props 요소 -->
    <!-- getAnimalImage는 자식 요소에 있고, emit을 사용해 부모요소에서 사용할 수 있다. -->
    <!-- getImage는 App.vue의 methods -->
    <GetImage btnName="멍멍" @getAnimalImage="getImage"/>
    <GetImage btnName="야옹" @getAnimalImage="getImage"/>
    <!-- animalUrl은 App.vue의 data로 v-bind를 통해 img태그와 연결해준다. -->
    <img v-bind:src="animalUrl" alt="">
  </div>
</template>

<script>
// import GetDogImage from './components/GetDogImage.vue'
// import GetCatImage from './components/GetCatImage.vue'
import GetImage from './components/GetImage.vue'
// axios를 사용하므로 import 해줘야 한다.
import axios from 'axios'

export default {
  name: 'app',
  components: {
    // GetDogImage,
    // GetCatImage,
    GetImage
  },
  methods: {
    getImage: function(name){
      // console.log("이벤트 발생")
      // console.log(name)
      if (name === "멍멍") {
        const DOG_URL = "https://dog.ceo/api/breeds/image/random"
        axios.get(DOG_URL)
          .then((response)=>{
            // data animalUrl에 url정보를 저장해준다.
            this.animalUrl = response.data.message
          })
          .catch((error)=>{
            console.log(error)
          })
      } else {
        const CAT_URL = "https://api.thecatapi.com/v1/images/search"
        axios.get(CAT_URL)
          .then((response)=>{
            this.animalUrl = response.data[0].url
          })
          .catch((error)=>{
            console.log(error)
          })
      }
    }
  },
  data: function(){
    return {
      animalUrl: ''
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
