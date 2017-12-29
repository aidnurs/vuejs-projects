<template lang="html">
  <div class="" >
    <button @click="addNumber(1)" v-bind:class="{ active: isBoxOneActive}">1</button>
    <button @click="addNumber(2)" v-bind:class="{ active: isBoxTwoActive}">2</button>
    <button @click="addNumber(3)" v-bind:class="{ active: isBoxThreeActive}">3</button>
    <button @click="addNumber(4)" v-bind:class="{ active: isBoxFourActive}">4</button>
    {{arr}}
    {{input}}
    {{trueStory}}
    <button @click="start" id="start">start</button>
    <!--<button @click="restart">restart</button>-->
    <button @click="stop" id="stop">stop</button>

  </div>
</template>

<script>
export default {
  data() {
    return {
      input: [],
      arr: [],
      number: 0,
      trueStory: true,
      userTurn: false,
      isBoxOneActive: false,
      isBoxTwoActive: false,
      isBoxThreeActive: false,
      isBoxFourActive: false,
      timer: 0,
      game: true
    };
  },
  mounted() {},
  methods: {
    start() {
      if (this.game) {
        this.generate();
        this.userTurn = true;
        this.showNumbers();
        this.game = false;
      }
    },
    restart() {
      this.arr = [];
      this.trueStory = true;
      this.start();
    },
    stop() {
      this.arr = [];
      this.input = [];
      this.trueStory = true;
      this.game = true;
    },
    addNumber(a) {
      if (this.trueStory && this.userTurn) {
        this.input.push(a);
        this.check();
      }
    },
    check() {
      for (var i = 0; i < this.input.length; i++) {
        if (this.arr[i] === this.input[i]) {
          this.trueStory = true;
        } else {
          this.trueStory = false;
          this.input = [];
          break;
        }
      }
      if (this.arr.length === this.input.length) {
        this.input = [];
        this.generate();
        this.showNumbers();
      }
    },
    generate() {
      if (this.trueStory) {
        this.number = Math.floor(Math.random() * 4) + 1;
        this.arr.push(this.number);
        this.number = 0;
      }
    },
    showNumbers() {
      this.userTurn = false;
      var self = this;
      var i = 0;
      self.timer = setInterval(function() {
        if (i >= self.arr.length) {
          self.stopInterval();
        }
        self.clickEffect(self.arr[i]);
        i++;
      }, 700);
    },
    stopInterval: function() {
      clearInterval(this.timer);
      this.userTurn = true;
    },
    clickEffect: function(boxNum) {
      var self = this;
      switch (boxNum) {
        case 1:
          this.isBoxOneActive = true;
          setTimeout(function() {
            self.isBoxOneActive = false;
          }, 300);
          break;
        case 2:
          this.isBoxTwoActive = true;
          //audio2.play();
          setTimeout(function() {
            self.isBoxTwoActive = false;
          }, 300);
          break;
        case 3:
          this.isBoxThreeActive = true;
          //audio3.play();
          setTimeout(function() {
            self.isBoxThreeActive = false;
          }, 300);
          break;
        case 4:
          this.isBoxFourActive = true;
          //audio4.play();
          setTimeout(function() {
            self.isBoxFourActive = false;
          }, 300);
          break;
      }
      return;
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
  background-color: red;
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
#start{
  border-radius: 100%;
  background-color: #32CD32;
}
#stop{
  border-radius: 100%;
  background-color: #FF4500;
}
button:active{
  transform: translate3d(4px);
}
.big{
  width: 100px;
  height: 100px;
}
.active {
  background-color: hsl(50, 50%, 10%);
}
</style>
