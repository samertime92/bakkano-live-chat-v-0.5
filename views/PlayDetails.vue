<template>
    <NavAccount :owning="owner" />
<div  v-if="error4" class="error">{{error4}}</div>
<div v-if="playlist">
      <div v-if="ownership">
          {{ownership}}{{owner}}

    <img :src="playlist.coverUrl" alt="">
    </div>
</div>
  <h2>playlist details. ID {{ id }}</h2>
  
</template>

<script>
import getDocument from '../composables/getDocument.js'
import { computed ,ref } from 'vue'
import getUser from '../composables/getUser.js'
import NavAccount from '../components/NavAccount.vue'
// import List from '../components/List.vue'

export default {
    name: "PlayDetails",
props :['id'],
 components: {NavAccount},
//  emits :['shit'],
setup(props){
      const {error4 ,document:playlist} = getDocument('userPhoto',props.id)

      const {user} = getUser()

      const ownership = computed(() =>{
          return user.value.uid == playlist.value.userId
          
         })
          

    const owner =ref('')
           function asshole(){
            if(ownership){
           owner.value = 'true'
         }
         else{
           owner.value = false
         }
           }
           setTimeout(asshole,1)
        //  setInterval(asshole,4000)
        console.log(ownership)
        console.log(owner)


return {error4 , playlist ,ownership,owner}
}
}
</script>

<style>

</style>