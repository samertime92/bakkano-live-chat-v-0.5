<template >

<!-- <B1DetailsES  @keep="keep2" /> -->
<div id="section1">
  <div v-if="!es">
<NavbarMaines/>
  </div>
  <div v-if="es">
<NavbarMain  />
</div>

<div v-if="cate">
<div v-if="!cate.items.length">
 <h1>nothing added yet</h1>
</div>

<div v-for="item in cate.items" :key="item.id">
  <h1>{{item.title}}
      {{item.price}}
  </h1>
</div>
</div>





</div>
<div id="section2">
  <img  class="img2" src="../assets/bakkano3d2.png" alt="">

</div>

<div id="section3">
  <div class="welcome container">
      <p>WELCOME TO BAKKANO</p>
<transition name="fade">
    <div v-if="ShowLogin">
      <h2>Login</h2>
    <LoginForm @logging ="enterChat"/>
      <P>No account yet  <span   @click="ShowLogin = false">Sign up </span>instead</P>
      </div>



      <div v-else>
        <h2>Sign up</h2>
    <SignupForm @signing ="enterChat"/>
      <P id="regPar">Already registered ?  <span id="fuck" @click="ShowLogin = true " >Login </span>instead</P>

        </div>
          </transition>


        
  </div>
  </div>
  <div id="section5">
        <Bevents :ev="eve" :ev2 ="eve2" />
        <div v-if="error" class="error">Could not bring data</div>
        <!-- <div v-if="documents"> -->
          <!-- <div v-for=" doc in eventlist" :key="doc.id"> -->
            <BakkanoEvents />
          </div>
        <!-- </div> -->
<!-- </div> -->
<div id="section6">
  <transition name="lanTr">
  <img v-if="enIcon" @click="esp" id="es" src="../assets/es.png" alt="">
  </transition>
  <transition name="lanTr">

  <img v-if="!enIcon"  @click="eng" id="en" src="../assets/en.png" alt="">
  </transition>

</div>
<!-- <div v-show="hideMe"> -->
<!-- </div> -->

</template>

<script>
// import getCollections from '../composables/getCollections'

import Bevents from  '../components/Bevents.vue'
import NavbarMain from  '../components/NavbarMain.vue'
import NavbarMaines from  '../components/NavbarMaines.vue'
// import B1DetailsES from  '../views/B1DetailsES.vue'

import BakkanoEvents from  '../components/BakkanoEvents.vue'
import SignupForm from  '../components/SignupForm.vue'
import LoginForm from  '../components/LoginForm.vue'
import {ref} from 'vue'
import { useRouter } from 'vue-router'
import getDocument from '../composables/getDocument'
import B1DetailsES from '../views/B1DetailsES.vue'

export default {
  // emits :['keep'],
  name:'Welcome',
components : { SignupForm, LoginForm , NavbarMain , Bevents, BakkanoEvents, NavbarMaines, B1DetailsES },
setup() {
  


const eve2 = ref(' AMAMOS LOS EVENTOS ')
const eve = ref(false)

const enIcon =ref(false)
const es =ref(false)
function windscro(){
window.scroll({
  top: 0,
  left: 0,
  behavior: 'smooth'
});
}
function windscro0(){
window.scroll({
  top: 10000,
  left: 0,
  behavior: 'auto'
});
}

const esp = () =>{

  
 eve2.value = ' AMAMOS LOS EVENTOS '
eve.value =! eve.value 
 setTimeout(windscro0 , 0);

 setTimeout(windscro , 350);
enIcon.value =! enIcon.value
  es.value =! es.value
  document.getElementById('section2').style.filter="blur(0px)"
  document.getElementById('section2').style.transform="translateY(0%)"
  
}
const eng = () =>{
 eve.value = ' WE LOVE EVENTS '
eve2.value =! eve2.value 

 setTimeout(windscro0 , 0);

 setTimeout(windscro , 350);

enIcon.value =! enIcon.value

  es.value =! es.value

  document.getElementById('section2').style.filter="blur(0px)"
  document.getElementById('section2').style.transform="translateY(0%)"

}
  const router = useRouter()
  const ShowLogin = ref(true)
  // const { error, documents } = getCollections('eventlist')
  const enterChat = () => {
    router.push({name:'Account'})
  }
  return { ShowLogin , enterChat , eve ,eve2 , es , esp , enIcon ,eng }
  
  }
}


</script>



<style >
.lanTr-enter-active,.lanTr-leave-active{
  transition: all 0.5s ease;
}

.lanTr-enter-from{transform:scaleY(0.3)rotate(300deg);opacity: 0;}
.lanTr-leave-to{transform: scaleY(0.3) rotate(300deg);opacity:0}

#es{width:23% ;margin: 0 auto;transition:0.4s;  }
.es:hover{width:18% ;margin: 0 auto; filter:drop-shadow(1px 1px 2px red)}
#en{width:23% ;margin: 0 auto;transition:0.4s; }
.en:hover{width:18% ;margin: 0 auto; filter:drop-shadow(1px 1px 2px red)}

.section2{transition:all 1s ease ;}
.section1{display:block;position: relative;margin-bottom: 40px;}
.fade-enter-from{opacity:0;}
.fade-enter-to{opacity:1;}
.fade-enter-active{ transition: opacity 1s ease-out }

.welcome{ z-index:1;
  border-bottom-right-radius: 100px;
    text-align: center;
    padding:20px 0;
}
.welcome form{ border-bottom-right-radius: 100px;;z-index:1;
  width:280px;
margin:20px  auto;}
.welcome .form2{ border-bottom-right-radius: 100px;;z-index:1;
  width:290px;
margin: 20px  auto;}
.welcome label {
  display: block;
  margin:20px 0 10px;
}
.welcome input {
  width: 100%;
  padding:10px;
  border-radius:20px;

  border: 2px groove red;
  outline:none;
  color:grey;
  margin:10px auto;
}
.welcome span{
  text-decoration:underline;
  font-weight: bolder;
  color:red;
  cursor:pointer
}

.welcome button{margin:20px auto;}
@media only screen and (min-width:320px){
#section1{display:block;position: relative;margin-bottom: 40px;}
#section2{transition: all 1 ease; display:block;position: relative;margin: 20px 0px 20px 0px;top:0px;}
#section3{display:block;position: relative;margin: 50px 0px 50px 0px;top:0px;padding-bottom:50px;top:20px;}
#section4{display:block;position: absolute;margin: 50px auto 50px auto;top:0px;padding-bottom:50px;top:26px;}
#section6{display:block;margin: 0px auto 30px auto;}

  .welcome.container{ z-index: 1;
    font-weight: bolder;
    background-color: white;
    width:90%;
    max-width:960px;
    margin: 5px auto;
    border-radius:20px;
    box-shadow:2px 4px  6px rgba(214, 8, 8, 1)
}
  .img2 {
    width: 44%;
    position: relative;
    z-index: 0;
    left: 0px;
    margin: 0px;
}

 
  .welcome{ z-index: 1;
  border-bottom-right-radius: 100px;
    text-align: center;
    padding:20px 0;
    height:300px;
    background: url(../assets/background2C.png);
    background-size: 300px;
    background-position: center;
    background-position-y: top;
    /* background-blend-mode: luminosity; */
}
.navbar[data-v-47330b99] {
    background-position: center;
    background-size: 2000px;
    padding: 1px 10px;
    margin-bottom: 10px;
    /* background:url(../assets/bakkano3d2.png); */
    background-position-x: center;
    background-size:100px; 
    background-repeat: no-repeat; 
    background-color: white;
    border-radius: 0px;
}
.welcome input {
  width: 50%;
  padding:10px;
  border-radius:20px;
  background-color: none;
  opacity: 50%;;

  border: 2px groove red;
  outline:none;
  color:grey;
  margin:10px auto;
}
#regPar{display: block; position: absolute;top:345px;margin:5px auto;padding:5px auto;left:20px;}
}
</style>