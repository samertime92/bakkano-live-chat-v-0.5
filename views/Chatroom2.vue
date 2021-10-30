<template>
<div v-if="user">
<h1> Welcome  to chatroom Bakkano   <br>   {{ user.displayName }}!!!  <br><br></h1>
</div>
<div v-if="document">
<h3>{{document.alls.length}} users <span class="spa1"> online</span></h3>
</div>
<div class="container">
<Navbar :loogy="id"/>
<hr>
<ChatWindow2 />
<hr>
<NewChat />
</div>
<div v-if="documents">
<div v-for ="doc in documents" :key="doc.id">
 <h2 v-if="doc.allUsersIds2">{{doc.allUsersIds2}} entered the room <br><br></h2>
   </div>
   </div>
   <div v-if="documents">
<div v-for ="doc in documents" :key="doc.id">
 <h2 v-if="doc.userLeft2">{{doc.userLeft2}} left the room <br><br></h2>
   </div>
   </div>
</template>

<script>
import getCollection from '../composables/getCollection'

import Navbar from '../components/Navbar.vue'
import NewChat from '../components/NewChat.vue'
import ChatWindow2 from  '../components/ChatWindow2.vue'
import getDocument from '../composables/getDocument'

import getUser from '../composables/getUser'
import {watch} from 'vue'
import { useRouter } from 'vue-router'
export default {
    components: {Navbar, NewChat, ChatWindow2},
    props:['id'],
    setup(){
 const {document} =  getDocument('bam','Z88rLYmZafHOcbQlcGWd')

const {documents} = getCollection('bam')
const {user} = getUser()
const router = useRouter()
watch (user, () =>{
    if(!user.value){
       router.push({ name:'Welcome' })
    }
})
    return {user, documents, document }

    }
}
</script>

<style scoped>
h3{   border-radius:10px;filter:drop-shadow(1px 1px 1px rgb(255, 254, 254) );
  font-size: 30px;
  background: linear-gradient(rgb(255, 255, 255), #333);
 background-clip: text;
 color: transparent;
}
h1{ box-shadow:0px 15px 20px rgba(255, 0, 0, 0.322)  ;border-radius:50px;filter:drop-shadow(1px 1px 1px rgb(255, 0, 0) );
  font-size: 40px;
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
.spa1{ background: linear-gradient(rgb(255, 2, 2), rgb(185, 3, 3), #333);
 background-clip: text;
 color: transparent;}
</style>