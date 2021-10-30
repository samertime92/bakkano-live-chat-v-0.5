<template>
<div v-if="user">
<h1>Bienvenido a la sala de chat Bakkano 2.0   <br>   {{ user.displayName }}!!!  <br><br></h1>
</div>
<div v-if="document">
<h3>{{document.alls.length}} users <span class="spa1"> online</span></h3>
</div>
<div class="container">
<NavbarEs  @out ="outNow"/>
<hr>
<ChatWindow :nowOut="outNow"/>
<hr>
<NewChatFormEs  />
</div>
<div v-if="documents">
<div v-for ="doc in documents" :key="doc.id">
 <h2 v-if="doc.allUsersIds">{{doc.allUsersIds}} ha entrado la sala <br><br></h2>
   </div>
   </div>
   <div v-if="documents">
<div v-for ="doc in documents" :key="doc.id">
 <h2 v-if="doc.userLeft">{{doc.userLeft}} ha salido de la sala <br><br></h2>
   </div>
   </div>
</template>

<script>
import NavbarEs from '../components/NavbarEs.vue'
import NewChatFormEs from '../components/NewChatFormEs.vue'
import ChatWindow from  '../components/ChatWindow.vue'
import getCollection from '../composables/getCollection'
import getDocument from '../composables/getDocument'

import getUser from '../composables/getUser'
import {ref, watch} from 'vue'
import { useRouter } from 'vue-router'
export default {
    components: {NavbarEs, NewChatFormEs, ChatWindow},
    setup(){
        const outNow = ref(false)
const {documents} = getCollection('bam')
    
    const {document} =  getDocument('bam','d9ZjhgO18GGwmbfkwOdS')

const {user} = getUser()
const router = useRouter()
watch (user, () =>{
    if(!user.value){
       router.push({ name:'WelcomeEs' })
    }
})
    return {user ,outNow,documents, document}

    }
}
</script>

<style scoped>
.spa1{ background: linear-gradient(rgb(255, 2, 2), rgb(185, 3, 3), #333);
 background-clip: text;
 color: transparent;}
h1{ box-shadow:0px 15px 20px rgba(255, 255, 255, 0.322)  ;border-radius:50px;filter:drop-shadow(1px 1px 1px rgb(255, 254, 254) );
  font-size: 38px;
  background: linear-gradient(rgb(255, 255, 255), #333);
 background-clip: text;
 color: transparent;
}
h2{ box-shadow:0px -15px 20px rgba(255, 255, 255, 0.322)  ;border-radius:50px;filter:drop-shadow(1px 1px 1px rgb(255, 254, 254) );
  font-size: 20px;
  background: linear-gradient(rgb(255, 255, 255), #333);
 background-clip: text;
 color: transparent;
}
h3{   border-radius:10px;filter:drop-shadow(1px 1px 1px rgb(255, 254, 254) );
  font-size: 30px;
  background: linear-gradient(rgb(255, 255, 255), #333);
 background-clip: text;
 color: transparent;
}
</style>