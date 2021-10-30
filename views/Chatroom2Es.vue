<template>
<div v-if="user">
<h1> Bienvenido a la sala de chat Bakkano  <br> {{ user.displayName }}!!!</h1>
</div>
<div v-if="document">
<h3>{{document.alls.length}} usuarios <span class="spa1"> en linea</span></h3>
</div>
<div class="container">
<NavbarEs :loogy="id"/>
<hr>
<ChatWindow2 />
<hr>
<NewChatEs />
</div>
<div v-if="documents">
<div v-for ="doc in documents" :key="doc.id">
 <h2 v-if="doc.allUsersIds2">{{doc.allUsersIds2}} ha entrado la sala <br><br></h2>
   </div>
   </div>
   <div v-if="documents">
<div v-for ="doc in documents" :key="doc.id">
 <h2 v-if="doc.userLeft2">{{doc.userLeft2}} ha salido de la sala <br><br></h2>
   </div>
   </div>
</template>

<script>
import getCollection from '../composables/getCollection'

import NavbarEs from '../components/NavbarEs.vue'
import NewChatEs from '../components/NewChatEs.vue'
import ChatWindow2 from  '../components/ChatWindow2.vue'
import getDocument from '../composables/getDocument'

import getUser from '../composables/getUser'
import {watch} from 'vue'
import { useRouter } from 'vue-router'
export default {
    components: {NavbarEs, NewChatEs, ChatWindow2},
     props:['id'],
    setup(){
 const {document} =  getDocument('bam','Z88rLYmZafHOcbQlcGWd')

const {user} = getUser()
const router = useRouter()
const {documents} = getCollection('bam')

watch (user, () =>{
    if(!user.value){
       router.push({ name:'WelcomeEs' })
    }
})
    return {user,documents,document }

    }
}
</script>

<style scoped>
.spa1{ background: linear-gradient(rgb(255, 2, 2), rgb(185, 3, 3), #333);
 background-clip: text;
 color: transparent;}
h3{   border-radius:10px;filter:drop-shadow(1px 1px 1px rgb(255, 254, 254) );
  font-size: 30px;
  background: linear-gradient(rgb(255, 255, 255), #333);
 background-clip: text;
 color: transparent;
}
h1{ box-shadow:0px 15px 20px rgba(255, 0, 0, 0.322)  ;border-radius:50px;filter:drop-shadow(1px 1px 1px rgb(255, 0, 0) );
  font-size: 38px;
  background: linear-gradient(rgb(255, 0, 0), #333);
 background-clip: text;
 color: transparent;
}
h2{ box-shadow:0px -15px 20px rgba(255, 0, 0, 0.322)  ;border-radius:50px;filter:drop-shadow(1px 1px 1px rgb(255, 0, 0) );
  font-size: 20px;
  background: linear-gradient(rgb(255, 0, 0), #333);
 background-clip: text;
 color: transparent;
}
</style>