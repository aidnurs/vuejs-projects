<template lang="html">
    <div class="main">
    	<div class="quarter quarter1"></div>
    	<div class="quarter quarter2"></div>
    	<div class="quarter quarter3"></div>
    	<div class="quarter quarter4"></div>
    	<div class="cutout"></div>
    </div>
</template>

<script>
import bell from './bell.vue'
export default {
  components:{bell}
}
</script>

<style lang="css">
#red{
  background-color: red;
}
#yellow{
  background-color: yellow;
}
#blue{
  background-color: blue;
}
#green{
  background-color: green;
}
.main {
	position:relative;
	width:200px;
	height:200px;
	margin:0 auto;
}

.quarter {
	position:absolute;
	width:50%;
	height:50%;
	transition:background-color 0.2s ease-in-out;
}
.quarter:hover {
	background-color:pink;
}
.quarter1 {
	top:0;
	left:0;
	background-color:red;
	border-radius:100% 0 0 0;
}
.quarter2 {
	top:0;
	right:0;
	background-color:blue;
	border-radius:0 100% 0 0 ;
}
.quarter3 {
	bottom:0;
	left:0;
	background-color:orange;
	border-radius:0 0 0 100%;
}
.quarter4 {
	bottom:0;
	right:0;
	background-color:green;
	border-radius:0 0 100% 0 ;
}
.cutout {
	width:50%;
	height:50%;
	background-color:white;
	position:absolute;
	top:25%;
	left:25%;
	border-radius:50%;
	pointer-events:none;
	}
</style>
