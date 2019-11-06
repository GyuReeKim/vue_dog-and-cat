<template>
  <!-- click event는 onAnimalImage methods와 연결되어있다. -->
  <!-- btnName은 props 요소로, 변수처럼 사용 가능하다. -->
  <button v-on:click="onAnimalImage">{{btnName}}</button>
</template>

<script>
export default {
  props: {
    btnName: String,
  },
  data: function(){
    return {
      
    }
  },
  methods: {
    onAnimalImage: function(){
      // 이벤트를 올리는 과정
      console.log(this.btnName)
      // emit은 자식요소를 부모에서 사용할 수 있도록 해준다.
      this.$emit('getAnimalImage', this.btnName)
    }
  }
}
</script>

<style>

</style>