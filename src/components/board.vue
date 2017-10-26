<template lang="html">
  <div class="">
    <button @click="addNumber(but)" v-for="(but,index) in buttons">{{but}}</button>
    {{arr}}
    {{input}}
    {{trueStory}}
  </div>
</template>

<script>
export default {
  data(){
    return {
      buttons:[1,2,3,4],
      input:[],
      number:0,
      arr:[1],
      trueStory:false,
    }
  },
  methods:{
    addNumber(a){
      this.input.push(a);
      this.check();
      this.generate();
    },
    check(){
      if (this.arr===this.input) {
        trueStory=true;
      }
    },
    generate(){
      this.number=Math.floor(Math.random() * 4)+1;
      this.arr.push(this.number);
      this.number=0;
    }
  }
}
</script>

<style lang="css">
</style>
