<template>
<div v-for="doc in pic " :key="doc.id">
  <img :src="doc.coverUrl" alt="">
  <h1> he is  {{nameit}}</h1> 
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import getCollection from '../composables/getCollection.js'

export default {
  props: ['id','nameit'],

setup(props){

  console.log(props.id)
  const squash = ref([props.id , props.value])
  console.log(squash)
   const {documents:pic} = getCollection('userPhoto',
       ['userId','==', props.id]) 

       return {pic}
}
} 
</script>

<style>

</style>