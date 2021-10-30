<template>
<!-- <transition name="evtr"> -->
  <h1  v-if="ev">{{ev}}</h1>
<!-- </transition> -->
<!-- <transition name="evtr"> -->
  <h2 v-if="ev2">{{ev2}}</h2>
<!-- </transition> -->

<div id="mainEvent">
  <form action="">



  </form>

</div>
</template>

<script>
import { ref } from 'vue'
// import Child from "./Child.vue"
export default {
  // components: {Child},
props: ['ev' , 'ev2'],
setup(props){



}
}
</script>

<style scoped>
h1{ 
  font-size: 50px;
  background: linear-gradient(#eee, #333);
  background-clip: text;
 color: transparent;
}
h2{
  font-size: 45px;
  background:linear-gradient(#eee, #333);
 background-clip: text;
  color: transparent;
}
/* .evtr-enter-active,.evtr-leave-active{ */
  /* transition: all 1s ease; */
/* } */
/* .evtr-enter-from{opacity:0} */

/* .evtr-leave-to{opacity:0} */

</style>