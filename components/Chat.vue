<template>
<div  class="chatBlock">
  <h1 v-if="!setEs">CHAT PEOPLE AROUND YOU   </h1>
  <h1 v-if="setEs">CHATEA CON GENTE ALREDADOR   </h1>
<div v-if="!setEs">
<div v-if="docum" @click="handleClick1" class="barDiv">  <span class="spa2">( {{docum.alls.length}} ) users online</span> <br> ENTER CHATROOM BAKKANO 1  </div>
  <div v-if="document" @click="handleClick" class="barDiv2"> <span class="spa1">  ( {{document.alls.length}} ) users online </span> <br> ENTER CHATROOM BAKKANO 2  </div>
  </div>
<div v-if="setEs">
<div v-if="docum" @click="handleClick3" class="barDiv">  <span class="spa2">( {{docum.alls.length}} ) usuarios en linea</span> <br> ENTRA AL CHATROOM BAKKANO 1  </div>
  <div v-if="document"  @click="handleClick0" class="barDiv2"> <span class="spa1">( {{document.alls.length}} ) usuarios en linea</span>  <br> ENTRA AL CHATROOM BAKKANO 2   </div>
</div>
  </div>
  <!-- <Login :setEs1="setLang1"/> -->
</template>

<script>
// import Login from '../components/Login.vue'
import { ref } from '@vue/reactivity'
import {useRouter} from 'vue-router'
import getDocument from '../composables/getDocument'
import getDocument2 from '../composables/getDocument2'

export default {
  // components : {Login},
  props:['setEs'],
    emits:['chatDirection','changeEve'],

setup(props, context){
    const {document} =  getDocument('bam','d9ZjhgO18GGwmbfkwOdS',)
    const {docum} =  getDocument2('bam','Z88rLYmZafHOcbQlcGWd',)

  const idd = ref('b78dyTrFsSw8NH4X7tF9')
  // const setLang1 = ref(false)
const router = useRouter()
const handleClick = () =>{
    router.push({name:'Login', params:{ id:idd.value}})
    // setLang.value = true
}
const handleClick0 = () =>{
    router.push({name:'LoginEs'})
    // setLang.value = true
    // context.emit('changeEve')
    // console.log('emitted')

}
const handleClick3 = () =>{
    router.push({name:'Login1Es'})
    // setLang.value = true
    // context.emit('changeEve')
    // console.log('emitted')

}


const handleClick1 = () =>{
    context.emit('chatDirection')
    router.push({name:'Login1'})


    
}
return { document, handleClick, handleClick1 , handleClick0 , handleClick3 ,docum}

}
}
</script>

<style scoped>
.spa1{padding:5px;border:solid  black 1px;border-radius:0px 20px 0px 0px;background:white;font-size:13px; float: left; filter:drop-shadow(3px 3px 2px rgba(0, 0, 0, 0.363))}
.spa2{ padding:5px;border:solid  rgb(255, 253, 253) 1px;border-radius:0px 0px 0px 20px;background:rgb(161, 3, 3);font-size:13px; float: right;  filter:drop-shadow(3px 3px 2px rgba(0, 0, 0, 0.363))}

.chatBlock{ margin:40px 0px 40px 0px  ;}
/* ;margin-bottom:10%;box-shadow:3px 3px 20px rgb(255, 255, 255); */
.barDiv{ z-index: 3; position:relative; float:left;display:block;width:70%;height:100%;  ;padding:50px 0px 50px 0px;position: relative;
transform:skewY(5deg);background:linear-gradient(0deg,white,white,white,white,white,white,white,white,white,rgba(255, 255, 255, 0.219))
;box-shadow:3px 10px 20px rgba(221, 127, 127, 0.651);font-weight:bolder;font-size:17px;color:rgb(255, 255, 255);text-decoration:none;font-family: monospace;border:1px;border-color:rgb(255, 0, 0);border-style:none;border-width:3px;
border-top-right-radius: 20px;border-bottom-right-radius: 20px;margin-bottom:10% ;;background: url(../assets/bakkano1log.png); background-size: 300px;
    background-position: center; background-repeat: no-repeat; background-color: aliceblue;} 
.barDiv2{ z-index: 3;  position:relative;
float:right;display:block;width:70%;height:100%;  ;padding:50px 0px 50px 0px;position: relative;
transform:skewY(5deg);background:linear-gradient(0deg,white,white,white,white,white,white,white,white,white,rgba(255, 255, 255, 0.219))
;box-shadow:3px 10px 20px rgba(255, 255, 255, 0.705);font-weight:bolder;font-size:17px;color:rgb(0, 0, 0);text-decoration:none;font-family: monospace;border:1px;border-color:rgb(238, 0, 0);border-style:none;border-width:3px;
border-top-left-radius: 20px;border-bottom-left-radius: 20px;margin-bottom:0%;
;background: url(../assets/people.png); background-size: 75px; background-position:bottom right; background-repeat:no-repeat; background-color:white;
} 
/* h1{font-size: 30px; color:red} */
h1{  text-decoration: none;
  font-size: 35px;
  background: linear-gradient(rgb(248, 242, 242),rgb(22, 22, 22));
  background-clip: text;
  -webkit-text-fill-color: transparent;}
  
</style>