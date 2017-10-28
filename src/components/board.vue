<template lang="html">
  <div class="" >
    <button
    @click="(trueStory)||(arr.length===1)?addNumber(but):null"
    v-for="(but,index) in buttons"
    ref="refs"
    v-bind:id="'color'+(++index)">{{but}}</button>
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
    this.showNumbers();
  },
  methods: {
    addNumber(a) {
      this.input.push(a);
      this.check();
      this.showNumbers();
    },
    check() {
      for (var i = 0; i < this.input.length; i++) {
        if (this.arr[i] === this.input[i]) {
          this.trueStory = true;
        } else {
          this.trueStory = false;
          break;
        }
      }
      if (this.arr.length === this.input.length) {
        this.input = [];
        this.generate();
      }
    },
    generate() {
      this.number = Math.floor(Math.random() * 4) + 1;
      this.arr.push(this.number);
      this.number = 0;
    },
    showNumbers() {
      /*function doSetTimeout(i) {
        setTimeout(function() {
          elem[[i]].classList.remove('big');
          //console.log(elem[i]);
        }, 1000);
      }
      var elem = this.$refs.refs;
      for (var i = 0; i < this.arr.length; ++i) {
        //console.log(elem[this.arr[i]-1]);
        //console.log(this.arr[i]);
        elem[this.arr[i] - 1].classList.add('big');
        doSetTimeout(this.arr[i] - 1);
      }*/
      for (var i = 0; i < this.arr.length; i++) {
        var elem = this.$refs.refs[this.arr[i] - 1];
        elem.classList.add('big');
        setTimeout(function() {
          elem.classList.remove('big');
        }, (  i+1)*1000);
      }
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
.big{
  width: 100px;
  height: 100px;
}
</style>
