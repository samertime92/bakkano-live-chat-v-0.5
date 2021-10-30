<template>
   <NavAccount />  
<div v-if="document">
  <h1>{{document.users.length}} signed up users</h1>
</div>
</template>

<script>

    import NavAccount from  '../components/NavAccount.vue'
  import getCollection from '../composables/getCollection'
import getUser from '../composables/getUser'
import List from '../components/List.vue'
import getDocument from '../composables/getDocument.js'
import { ref } from '@vue/reactivity'

export default {
components:{NavAccount,List},
name: 'Account',
setup(){
    const { document} = getDocument('signedUps','d44ff1tsGGbPWQN66LQA')

  const {user} = getUser()
  const {documents:pic} = getCollection('userPhoto',
  ['userId','==', user.value.uid]
  
  )
  
      const handleSubmit = () =>{
  //  const { error , addDoc} = useCollection('userinfo')
  
}



  return{ handleSubmit ,pic,document  }
}
}
</script>

<style scoped>
h1{  font-family:monospace;color:linear-gradient(black,black, white);padding:5px;border:none;border-radius:0px;background:white;font-size:13px; margin:0 auto;  filter:drop-shadow(1px 1px 2px rgba(255, 255, 255, 0.541))}

</style>