<template>
<transition name="show2">
  <div class="pri-div" v-if="hide0">
    <User :id="doo" :nameit="noo" @cancel0="cancel1" :acc="acception" @cool="cool1" @cool2="cool3" @allow="allow1" />
  </div>
  </transition>
  <div class="chat-window">
<!-- <div v-if="hide">  <h1>private mode</h1>  </div> -->
<div v-if="error3">{{error3}}</div>
<div  v-if="documents" class="messages" ref="messages">
  
    <div v-for="doc in formattedDocuments" :key="doc.id" class="single">

        <div class="div0">
 <!-- <router-link :to="{name:'user', params:{ id: doc.uidi, nameit: doc.name }}" > <span  class="name">{{doc.name}}</span></router-link>     -->
 <span v-if="!shot" @click="priShip(doc.uidi , doc.name )" class="name">{{doc.name}}</span> 

 <span  v-if="shot" @click="priShip2" class="name">{{doc.name}}</span>  


 <span class="created-at">{{doc.createdAt}}</span>
 <img class="imagin" :src="doc.pic" alt="its here">

 
 </div>
 <!-- <br><br> -->
 <!-- <div class="uImg" v-if="ass">
 <List :userPhoto="ass" />
 </div> -->
   <!-- <transition name="show"> -->
 <span  class="message">{{doc.message}}</span>



   <!-- </transition> -->
   
    </div>
 
  
</div>



 <!-- <span v-if="!nowOut"  class="Created-at">{{user.displayName}} left the chat room</span> -->
  </div>

</template>

<script>
import { useRouter } from 'vue-router'
import getCollection from '../composables/getCollection'
import { formatDistanceToNow} from 'date-fns'
import { computed , onUpdated, reactive, ref, toRefs, watch, watchEffect} from 'vue'
import getUser from '../composables/getUser'
import getIt from '../composables/getIt'
import useCollection from '../composables/useCollection'
import { timestamp } from '../firebase/config'
import useDocument from '../composables/useDocument'
import useDocument2 from '../composables/useDocument2'

import getDocument from '../composables/getDocument'
import getPri from '../composables/getPri'
import User from '../components/User'


//added
// import getUser from '../composables/getUser'
// import List from '../components/List.vue'
//out


export default {
    props:['nowOut','timeV','acception',],
    components:{ User },
    emits:['fab','fab2','allow2' ],

    // components:{List},
    setup(props , context){
     

      const cool1 =(uidi)=>{
        context.emit('fab',uidi)
      
     
      }
       const allow1 =()=>{
        context.emit('allow2')
      
     
      }
      const cool3 =(uid)=>{
        context.emit('fab2',uid)
      
      }
      
    const {addDoc, error2} = useCollection('priMessage')
    const { updateDoc} = useDocument('priMessage','f1UxTgzOArv697Aslbny')
    const { updateDocs} = useDocument2('priMessage','XptRT1gegDTa0rmA4DtS')

    const {  document:uipri } = getDocument('priMessage','f1UxTgzOArv697Aslbny')
    const {user} = getUser()
       const {pri} = getPri('priMessage','f1UxTgzOArv697Aslbny')
        const shot =ref(false)
        const bam = computed(()=>{
    return pri.value.uidA.length > 100
    })
    console.log(bam)
    // const cool= ref(bam)

    
//     watch( bam ,()=>{
//       console.log(bam)
// //       cool.value = bam
// //        if(cool){
// //               shot.value =true
// //               console.log('cool is one')
// //             }
// //             else {
// // console.log('cool isfalse')
// //             }
            
//     })
        const noo = ref(false)
        const doo = ref(false)

        const hide = ref(false)
        const hide0 = ref(false)
        const cancel1 = ()=>{
         hide0.value = false
         console.log('yeah')
  document.querySelector('.chat-window').style.filter = "blur(0px)brightness(100%)"


        }
        const priShip2=()=>{
          alert('chatroom is full')
        }
        const priShip= async (uidi , name)=>{
          if (bam.value == true){
            console.log ( 'chat is full')
          }
          else{
            console.log(uidi,'hey')
            hide.value = true
            console.log(shot,'hey')
           
      
        if(pri.value.uidA.includes(uidi , user.value.uid) ){
          console.log('blocked')
        }
  
        
        // const chatPriv = {
        //   uid : uidi,
        //     name: user.value.displayName,
        //     createdAt : timestamp(),
        // }
       

      // const signup = useSignup()
// const alls0 = ass.value.nameA.push(user.value.displayName)
else{
       await updateDocs({
          reject:true
            })
  hide0.value= true
  noo.value = name
  doo.value = uidi
  document.querySelector('.chat-window').style.filter = "blur(5px)brightness(75%)"

// const ui = uipri.value.uidA.push(uidi , user.value.uid)

// const uidA = uipri.value.uidA
//         await updateDoc({
//              uidA: uidA,

           

//             })
         
      }
          }
        }
        const timeval = ref('0')
   
   watchEffect(()=>{
 const d = new Date();
   const  time = d.getTime();
   console.log(time)
 timeval.value = time
   })
        console.log(timeval.value , 'ok')

//   const timeva = ref('fuck you')
//   timeva.value = timeval.value
// watchEffect(()=>{
//   timeva.value = timeval.value
// console.log(timeva.value)

// })
//   }
// const shit = ()=>{
//     console.log(timeva.value)
// } 

// setTimeout(timezone,0)
// setTimeout(shit, 5000)



//         const changeColor =()=>{
 
//     // if(user.)    const randomColor = Math.floor(Math.random()*16777215).toString(16);
//   document.getElementById('messager').style.color = "green";
//   console.log(' color-changed')
// //   color.innerHTML = "#" + randomColor;

        


        const formattedDocuments = computed(() => {
            if (documents.value){
                return documents.value.map( doc => {
                    let time = formatDistanceToNow(doc.createdAt.toDate())
                    return {...doc ,createdAt: time}

                })
            }

        })
         const timeSeq = computed(() => {
            if (documents.value){
                return documents.value.map( doc => {
                    let time =formatDistanceToNow(doc.createdAt.toDate())
                    // return {...doc ,createdAt: time}

                    return   time
                })
            }

        })
  
        
        const router = useRouter()
        const chatme = () =>{
            router.push({name:'user'})
        }
        
// var registry = Date.now();
// const {error3, documents} = getCollection('message')
const { pam } = getCollection('userPhoto')
       
const  {error3, documents} = getIt('message',
['timer','>=', timeval.value ])

const messages = ref(null)
// if(documents){
// onUpdated(() => {
//         messages.value.scrollTop = messages.value.scrollHeight
//     })
// }

   //added for change 


//ended 
return { allow1, cool3 ,cool1, cancel1,  noo , doo,hide0, shot, priShip2 ,hide, priShip , error3, documents ,formattedDocuments , messages ,user,pam}
    }
 
    }

</script>

  <style scoped>
  .pri-div{ padding: auto 10px; position:fixed;top:100px;margin:0px 60px 0px 50px;background:white;z-index:3;border-radius:10px ; box-shadow:3px 3px 10px white}
  .show2-enter-active{
  transition: all 0.5s ease;
}
.show2-leave-active {
    transition: all 0.5s ease-in;
}
.show2-enter-from{transform:scale(0.5);opacity: 0;}
.show2-leave-to{transform: scale(0.3);opacity:0}
  .pri{background-color:rgba(255, 0, 0, 0.37);border-radius:5px;font-size:8px;;float:right;color:white}
.imagin{width:100%; max-width:100%}
/* .div0{display: flex;justify-content:start;margin-bottom: 2%;} */
.div0{display: grid;grid-template-columns: 1fr 1fr 1fr;margin-bottom: 2%;grid-template-rows: 1fr;}

h1{background:linear-gradient(black,black,white);background-clip:text;color:transparent;margin-bottom:0; font-size:30px;}
.div1{display: flex;align-items: center;}
.message{background:linear-gradient(rgb(255, 0, 0),rgb(255, 0, 0));
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



.chat-window { transition:0.5s;
    background:rgb(255, 255, 255);
    padding:30px 20px;

}
.single{
    margin:19px 0px;
 background:linear-gradient(0deg,rgb(255, 255, 255),rgb(255, 255, 255), rgba(0, 0, 0, 0.048));border-radius: 10px;box-shadow: 2px 4px 3px rgba(0, 0, 0, 0.226);
}
.created-at {
    display: block;
    color:lightgray;
    font-size:12px;
    margin-bottom :4px;

}
.name{padding:1%;color:rgb(255, 255, 255);border-bottom-right-radius: 100px;border-top-left-radius: 15px;max-height:30px;
 background:linear-gradient(0deg,black ,black ,white);
 box-shadow: 3px 5px 5px rgba(0, 0, 0, 0.5);
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