<template>
 
  <div class="chat-window">
<div v-if="error">{{error3}}</div>
<div v-if="documents" class="messages" ref="messages">
  
    <div v-for="doc in formattedDocuments " :key="doc.id" class="single">
        <div class="div0">

        <span @click="chatme" class="name">{{doc.name}}</span>
 <span class="created-at">{{doc.createdAt}}</span>
 <img class="imagin" :src="doc.pic" alt="its here">

</div>
 <span  class="message">{{doc.message}}</span>

 <!-- <div class="uImg" v-if="ass">
 <List :userPhoto="ass" />
 </div> -->
 <!-- <span  class="message">{{doc.pic}}</span> -->
    </div>

</div>


  </div>
  
  
</template>

<script>
import { useRouter } from 'vue-router'
import getCollection from '../composables/getCollection'
import { formatDistanceToNow} from 'date-fns'
import { computed , onUpdated, ref, watchEffect} from 'vue'
import getUser from '../composables/getUser'
import getIt from '../composables/getIt'


//added
// import getUser from '../composables/getUser'
// import List from '../components/List.vue'
//out


export default {
    
    // components:{List},
    setup(){
        
//  const {user} = getUser()
 const {user} = getUser()
       const timeval = ref('0')
   
   watchEffect(()=>{
 const d = new Date();
   const  time = d.getTime();
   console.log(time)
 timeval.value = time
   })
        console.log(timeval.value , 'ok')
        
        const formattedDocuments = computed(() => {
            if (documents.value){
                return documents.value.map( doc => {
                    let time = formatDistanceToNow(doc.createdAt.toDate())
                    return {...doc ,createdAt: time}
                })
            }

        })
        
        const router = useRouter()
        const chatme = () =>{
            router.push({name:'user'})
        }
        

// const {error3, documents} = getCollection('message2')
const  {error3, documents} = getIt('message2',
['timer','>=', timeval.value ])

const { pam } = getCollection('userPhoto')



const messages = ref(null)

onUpdated(() => {
    messages.value.scrollTop = messages.value.scrollHeight
})

   //added for change 


//ended 
return { error3, documents, chatme,formattedDocuments , messages ,pam }
    }
 
    }

</script>

<style scoped>
.imagin{width:100%; max-width:100%}
/* .div0{display: flex;justify-content:start;margin-bottom: 2%;} */
.div0{display: grid;grid-template-columns: 1fr 1fr 1fr;margin-bottom: 2%;grid-template-rows: 1fr;}

h1{background:linear-gradient(rgb(255, 0, 0),black,white);background-clip:text;color:transparent;margin-bottom:0; font-size:30px;}
.div1{display: flex;align-items: center;}
.message{background:linear-gradient(black,grey);
background-clip:text;
color:transparent}
.show-enter-active{
  transition: all 0.5s ease;
}
.show-leave-active{
  transition: all 0s  step-end ;

}
.show-enter-from{transform:scaleY(0.3);opacity: 0;}
.show-leave-to{transform: scaleY(0.3);opacity:0}

.uImg{max-width: 10px; border-radius: 50px;}



.chat-window {
    background:url(../assets/bakkano1log.png);background-position: center;background-size: 220%;
    padding:30px 20px;

}
.single{
    margin:19px 0px;border-top-left-radius: 50px;
 background:linear-gradient(0deg,rgb(253, 192, 192),rgb(255, 255, 255), white);border-radius: 10px;box-shadow: 2px 4px 3px rgba(0, 0, 0, 0.226);
}
.created-at {
    display: block;
    color:lightgray;
    font-size:12px;
    margin-bottom :4px;

}
.name{padding:1%;color:rgb(255, 255, 255);max-height:30px;
 background:linear-gradient(0deg,rgb(116, 1, 1) ,rgb(255, 0, 0) ,white);border-bottom-right-radius: 15px;
 border-top-right-radius: 100px;
 box-shadow: 3px 5px 5px rgba(82, 1, 1, 0.5);
font-weight: bold;
margin-right: 6px;}
.messages{ text-align: left; width:100%;
    max-height: 400px;
    overflow:scroll;
    /* animation:change;
    animation-delay: 1s;
    animation-direction: normal;
    animation-fill-mode: forwards;
    animation-iteration-count: 1;
    animation-duration: 2s;
    animation-timing-function: ease;
}
@keyframes change{
    0%{display:none}
    100%{display:none} */
}
</style>