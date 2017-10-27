<template lang="html">
  <div class="" >
    <button @click="(trueStory)||(input.length===0)?addNumber(but):null" v-for="(but,index) in buttons" ref="refs" v-bind:id="'color'+(++index)">{{but}}</button>
    {{arr}}
    {{input}}
    {{trueStory}}
  </div>
</template>

<script>
export default {
  data() {
    return {
      buttons: [1, 2, 3, 4],
      input: [],
      number: 0,
      arr: [],
      trueStory: false
    };
  },
  mounted() {
    this.generate();
    //this.$refs.refs[0].click();
    //console.log(this.$refs.refs[0]);
  },
  methods: {
    addNumber(a) {
      this.input.push(a);
      this.check();
      this.generate();
    },
    check() {
      for (var i = 0; i < this.arr.length; i++) {
        if (this.arr[i] === this.input[i]) {
          this.trueStory = true;
        } else {
          this.trueStory = false;
          break;
        }
      }
    },
    generate() {
      this.number = Math.floor(Math.random() * 4) + 1;
      this.arr.push(this.number);
      this.number = 0;
    }
  }
};
</script>

<style lang="css">
button{
  margin: 10px;
  width: 50px;
  height: 50px;
}
#color1{
  background-color: ;
}
#color2{
  background-color: ;
}
#color3{
  background-color: ;
}
#color4{
  background-color: ;
}
button:hover{background-color: #3e8e41}
button:active{
  transform: translateY(4px);
}
</style>
