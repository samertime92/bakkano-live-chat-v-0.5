<template>

 <div v-if="user">
   <div v-if="guestList"></div>
     
<h1> Welcome  to chatroom Bakkano 2.0  <br>   {{ user.displayName }}!!!  <br><br></h1>
</div>
<div v-if="docker">
<h3>{{docker.alls.length}} users <span class="spa1"> online</span> <br> <img src="../assets/people1.png" alt=""></h3>
</div>
<div class="div3">
  <img @click="bringList" class="pep" src="../assets/people1.png">
  
<transition name="show2">
     <button  v-if="shit && !cleaner"  class="btn0" >
       <div> You received a private invitation </div><br>
         <div v-if="col && known">
<div v-for ="doc5 in col" :key="doc5.id">
  <img :src="doc5.coverUrl" alt="its here">
  <h1>{{doc5.userName}}</h1>
   </div>
   </div>
         <div v-if="!col && known">
          error
           </div>


  <div class="btns">
     <!-- <button  class="btn1" v-if="shit && !cleaner" @click="takenoPri"  ><img src="../assets/del.png" alt=""></button> -->

     <button class="btn"  v-if="shit  && known"  ><img src="../assets/change.png" alt=""></button>

   <div v-if="pri">
<div v-for ="doc3 in pri.owner" :key="doc3.id">
     <button  class="btn1" v-if="shit  && doc3.reciver === ids && !known" @click="takenoPri(doc3.id)"  ><img src="../assets/del.png" alt=""></button>
     <button class="btn" @click="handleIt(doc3.id)" v-if="doc3.reciver ===  ids && !known" ><img src="../assets/change.png"> </button>
   </div>
   </div>
</div>
     
      </button>
  </transition>
  <br> <br>


  <!-- <transition name="show2">
     <button  v-if="shit && cleaner && bringem && acceptionCheck " @click="takeUsPri1" class="btn" >  accepted </button>
  </transition> -->
     </div>
 
<div class="container">
   
<Navbar  @out ="outNow"/>
<hr>
<div v-if="!allows ">
<ChatWindow :nowOut="outNow" :acception ="acceptionCheck"  @fab="fab1"  @fab2="fab3" @allow2="allow3" />
</div>
<div v-if="allows && shit" >
<Prichat :key1="Nuid" :key2="Nuidi" :sender="theSender" :reciver="theReciver"/>
</div>
<br v-if="allows">
<div v-if="!allows">
<hr> 
<NewChatForm  />
</div>
</div>
<div v-if="documents">
<div v-for ="doc in documents" :key="doc.id">
 <h2 v-if="doc.allUsersIds">{{doc.allUsersIds}} entered the room <br><br></h2>
   </div>
   </div>
   <div v-if="documents">
<div v-for ="doc in documents" :key="doc.id">
 <h2  v-if="doc.userLeft">{{doc.userLeft}} left the room <br><br></h2>
   </div>
   </div>
</template>

<script scoped>
import getCollection from '../composables/getCollection'
import getCol from '../composables/getCol'

import getCollections from '../composables/getCollections'
import getPri from '../composables/getPri'
import getPri2 from '../composables/getPri2'
import Prichat from '../components/Prichat.vue'
import useDocument from '../composables/useDocument'
import useDocument2 from '../composables/useDocument2'

import Navbar from '../components/Navbar.vue'
import NewChatForm from '../components/NewChatForm.vue'
import ChatWindow from  '../components/ChatWindow.vue'
import PriChatWindow from  '../components/PriChatWindow.vue'
import getDocument from '../composables/getDocument'
import getDocument2 from '../composables/getDocument2'

import getUser from '../composables/getUser'
import {computed, isReactive, reactive, ref, toRefs, watch,watchEffect} from 'vue'
import { useRouter } from 'vue-router'
import {
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
  onActivated,
  onDeactivated,
  onErrorCaptured
} from "vue";

export default {
    components: {Navbar, NewChatForm, ChatWindow , PriChatWindow , Prichat},
 

    setup(props, context){

      window.addEventListener('beforeunload', function (e) {
allows.value=false

        
});

// onBeforeMount(()=>{
// alert('fuckyou1')
// })
// onUpdated(()=>{
// alert('fuckyou2')
// })
// onBeforeUnmount(()=>{
// alert('fuckyou2')
// })
// onBeforeMount(()=>{
//   function dodo(){
// const condition3 = pri.value.owner.find(()=> doc3.id == id )
//  console.log(condition3)
// alert('fuckyou3')

//   }
//   setTimeout(dodo,4000)
 

  
// })


      const guestList = ref(true)
      const known = ref(false)
      
      const Nuid = ref(false)
  const Nuidi = ref(false)

     const fab1 = (uidi)=>{
       Nuidi.value = uidi
      // const Nuidi = uidi

      }
      const allow3= ()=>{
       allows.value =true
      // const Nuidi = uidi

      }

  

      
      

    //   const shiter2= ref(shiter)

    //   console.log(fab1)
      const fab3 =(uid)=>{
        Nuid.value = uid
    //   console.log(Nuid.value)
      }
  watchEffect(()=>{
      console.log(Nuid.value)
      })
  watchEffect(()=>{
      console.log(Nuidi.value)

      })

    //    console.log(shiter)
    
    //    return shiter
    
        // 'd9ZjhgO18GGwmbfkwOdS'
// const { updateDoc} = useDocument('bam','d9ZjhgO18GGwmbfkwOdS')

    const {document:docker} =  getDocument('bam','d9ZjhgO18GGwmbfkwOdS')
    const {docum} =  getDocument2('priMessage','XptRT1gegDTa0rmA4DtS')
    const acceptionCheck = computed(()=>{
        return docum.value && docum.value.accept == true
    })
    
       console.log(acceptionCheck)
  
//   console.log(alls.length)
        const outNow = ref(false)
const {documents} = getCollection('bam')
// const {documents} = getCollection('bam')
const priv = ref(false)
const {pri} = getPri('priMessage','f1UxTgzOArv697Aslbny')
// const {pri} = getPri2('priMessage','f1UxTgzOArv697Aslbny')
    const {updateDoc} = useDocument('priMessage','XptRT1gegDTa0rmA4DtS')
    const {updateDocs} = useDocument2('priMessage','f1UxTgzOArv697Aslbny')

console.log(pri)
const docum2 = ref(null)
// watch(pri,()=>{
//       if(pri){
//      const docum3 = pri.value.owner
//     console.log(docum3)
//     docum2.value = docum3
//       }
//     })
const theSender = ref(false)
const theReciver = ref(false)
const amongThem= ref(false)
// const amongThem =ref(false)
     
         const handleIt= async(id)=>{
          //  known.value = true
 const gotya = pri.value.owner.find((doc3)=> doc3.id == id ).sender
 const gotya2 = pri.value.owner.find((doc3)=> doc3.id == id ).reciver
 const condition = pri.value.owner.find((doc3)=> doc3.id == id ).reject=false


console.log(id)
console.log(gotya)
console.log(gotya2)
const owner = pri.value.owner
condition.value !=condition.value

await updateDocs({owner})
 theSender.value= gotya
theReciver.value =gotya2
 amongThem.value = theSender
           console.log(theSender.value,'its here')
           setTimeout(takeUsPri,0)
           setTimeout(scro,1200)
       }
       function scro(){
         window.scroll({
           top:1000,
           left:0,
          behavior:'smooth'
           
         })
       }

  const {col} = getCol('userPhoto',
       ['userId','==', theSender.value])
         console.log(col,'doneeeeeeeee')
     
    //  watch(theSender,()=>{
    //    const {col} =getCol('userPhoto',
    //    ['userId','==', theSender.value])
    //    console.log(col , 'newval')
    //  })
     
       watchEffect(()=>{
         console.log(theSender.value,'sender')
       })
       
       watchEffect(()=>{
         console.log(theReciver.value,'reciver')
       })
       
//   if (pri.length = false){
//         console.log('fuvk you')
//         priv.value = false
//     }
// else {
// console.log(pri)
//         priv.value = true

//     }
// } )



    
const {user} = getUser()
const userNum =ref('0')
const num =ref(false);
console.log(user.value.uid)
const newuse = ref('')
// console.log(counter) 
const ids = ref(user.value.uid )
console.log(ids.value,'those ids')
const idCol = ['0','2','3'];
watchEffect(()=>{
    
console.log( ids.value,'user entered')
})
watchEffect(()=>{
    idCol.push(ids.value)
}

)
console.log(idCol.length,)
console.log(idCol)


const router = useRouter()
watch (user, () =>{
    if(!user.value){
       router.push({ name:'Welcome' })
    }
})
watchEffect(() =>{
    if(user.value){
        num.value = userNum + 1;
console.log('fuck') 
    }
  
    
})
console.log(num.value) 
    // const {addDoc, error} = useCollection('usersIds')
//  watchEffect (async()=>{
//         // if(ids.value){
//             await addDoc({
//                allUseId : [] ,
//             })
//             console.log('watched')
        
//  });
const usr = user.value.uid

const shit = computed(()=>{
  
    return pri.value && usr && usr == pri.value.uidA.find(myfunc0)
    function myfunc0(act){
        return act  == user.value.uid
    }
  
 
})
const cleaner = computed(()=>{
    return pri.value && pri.value.owner.find(myfunc5)
     function myfunc5(item){
        return item.sender  == user.value.uid
    }
})
const shet = ref(false)



const takeUs = [null]
const allows = ref(false)
const bringem = ref(true)
   

const takeUsPri = async ()=>{
  
  document.querySelector('.btn').style.boxShadow = "7px 7px 1px rgb(26, 233, 112)";
  document.querySelector('.btn').style.filter = "brightness(130%)";
  document.querySelector('.btn').style.margin = "10px auto";
  document.querySelector('.btn0').style.animationPlayState = "running";


    allows.value =true
takeUs.value = [pri.value.uidA]
bringem.value = true
console.log(takeUs.value)
   await updateDoc({
  accept: true  
})
}

const close = async ()=>{
   await updateDocs({
          reject:true
            })
            
 }
const takenoPri = async (id)=>{
            // known.value = true
   document.querySelector('.btn1').style.boxShadow = "7px 7px 1px rgb(255, 255, 255)";
  document.querySelector('.btn1').style.filter = "brightness(130%)";
  document.querySelector('.btn1').style.margin = "10px auto";
  // document.querySelector('.btn1').style.animationPlayState = "running";

 const condition2 = pri.value.owner.find((doc3)=> doc3.id == id ).reject2 = true
const sorter = async()=>{
 const sortOut = pri.value.owner.filter((doc3)=> doc3.id != id )
 const destroySender = pri.value.owner.find((doc3)=> doc3.id == id ).sender
 const destroyReciver = pri.value.owner.find((doc3)=> doc3.id == id ).reciver
       function myfunc3(item){
   return item != destroySender

 }
      function myfunc4(item){
   return item != destroyReciver

 }
 
  const uiDestroy = pri.value.uidA.filter(myfunc3).filter(myfunc4)
 await updateDocs({
 uidA: uiDestroy

  
})
await updateDocs({owner:sortOut})
}



const owner = pri.value.owner
// condition2.value != condition2.value
await updateDocs({owner})
setTimeout(sorter,3000)
    allows.value =false
bringem.value = false
//    await updateDoc({
//   accept: false  ,
//   reject: false,

// })

           setTimeout(scro,1200)



}
const takeUsPri1 = ()=>{
    allows.value =true
takeUs.value = [pri.value.uidA]
bringem.value = true
console.log(takeUs.value)
// router.push({name:'Prichat'})
}
const shit4 = ref(false)

   
 
watch(shit, ()=>{
  if(shit){
     window.scroll({
           top:0,
           left:0,
          behavior:'smooth'
           
         })
  }
  // if(!allows){
  // console.log(allows,'here')
  //   alert('shit')
  // }
  
})
const bringList = ()=>{
  document.querySelector('.div3').style.background="red"
  alert('shit')
}
 

    return {guestList,bringList, cleaner, allow3,col, known ,theReciver, theSender , pri , handleIt, docum2,Nuid ,Nuidi,acceptionCheck,takenoPri, takeUsPri1 , bringem , allows ,takeUs, takeUsPri , shit, user ,outNow ,documents ,docker , fab1,fab3 ,ids}

    }
}
</script>

<style scoped>
.btn0{box-shadow:7px 7px 2px rgba(202, 5, 5, 0.76); margin:5px;transform:skewX(-1deg);transition:0.4s;border-style:groove;border-width:1px;border-color:rgba(172, 16, 16, 0.486);border-right:none;border-bottom:none; display:flex; align-items: center;padding:5px;margin:0 auto}
.btn0{animation: btn00 0.5s forwards 1 paused 0.5s}
.btns{max-width:79px;}
@keyframes btn00{
    0%{box-shadow:7px 7px 2px rgba(202, 5, 5, 0.76) ;}
    20%{box-shadow:7px 7px 2px rgb(26, 233, 112) ;}
    30%{box-shadow:7px 7px 2px rgba(202, 5, 5, 0.76) ;}
    40%{box-shadow:7px 7px 2px rgb(26, 233, 112) ;}
    60%{box-shadow:7px 7px 2px rgba(202, 5, 5, 0.76) ;}
    65%{box-shadow:7px 7px 2px rgb(26, 233, 112) ;}
    70%{box-shadow:7px 7px 2px rgba(202, 5, 5, 0.76) ;}

    100%{box-shadow:7px 7px 2px rgb(26, 233, 112) ;}

}


.btn{box-shadow:7px 7px 2px rgba(202, 5, 5, 0.76); margin:5px 5px;transform:skewX(-1deg);transition:0.4s;border-style:groove;border-width:1px;border-color:rgba(172, 16, 16, 0.486);border-right:none;border-bottom:none}
/* .btn:hover{box-shadow:7px 7px 2px rgb(26, 233, 112); margin:5px 20px;transform:skewX(-1deg)} */
.btn1{box-shadow:7px 7px 2px rgba(202, 5, 5, 0.76); margin:5px 5px;transform:skewX(-1deg);transition:0.4s;border-style:groove;border-width:1px;border-color:rgba(172, 16, 16, 0.486);border-right:none;border-bottom:none}
/* .btn1:hover{box-shadow:7px 7px 2px rgb(255, 255, 255); margin:5px 20px;transform:skewX(-1deg)} */

.div3{ transition:1s;background:rgb(0, 0, 0)  ;opacity:1; border-radius:0px;box-shadow:0px 0px 10px rgba(255, 0, 0, 0.637)}

.show2-enter-active{
  transition: all 0.6s ease;
}
.show2-leave-active {
    transition: all 0.6s ease-in;
}
.show2-enter-from{transform:scale(0.3);opacity: 0;}
.show2-leave-to{transform: scale(0.3);opacity:0}
.spa1{ background: linear-gradient(rgb(255, 2, 2), rgb(185, 3, 3), #333);
 background-clip: text;
 color: transparent;}
h1{ box-shadow:0px 15px 20px rgba(255, 255, 255, 0.322)  ;border-radius:50px;filter:drop-shadow(1px 1px 1px rgb(255, 254, 254) );
  font-size: 40px;
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
h3{ transform:skewX(0deg);;  border-radius:10px;margin-bottom: 0px;
  font-size: 30px;padding:50px auto;
  background: linear-gradient(rgb(255, 255, 255), #333);
 background-clip:text;
 color: transparent ;
}
.pep{ filter: invert(100%);margin:12px auto 0px auto;}
</style>