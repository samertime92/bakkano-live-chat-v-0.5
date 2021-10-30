 
<template>
      <router-link id="nav" :to="{name:'WelcomeEs'}"><button class="btn" >Salir</button></router-link>

<div >
  <form @submit.prevent="handleSubmit">
      <input type="email" required placeholder="Email" v-model="email">
      <input type="password" placeholder="Contraseña" v-model="password">
      <p>{{error}}</p>
   <transition name="show">

       <div class="labeld" v-if="hidetxt">
  <label>  
      Por favor, acepte los términos marcando la casilla de verificación a continuación para fines de mantenimiento todos los messeges se envían a una base de datos creada por el gerente, por lo general los datos se eliminan después de un período de 30 días, por favor sea amable y no utilice lenguaje malo o agresivo
      no comparta su propia información real como número de teléfono, geolocalización u otra información privada con extraños a menos que desee     
  </label>
  </div>
   </transition>
 <transition name="show">

       <div class="labeld2" v-if="!hidetxt">

  <label > Gracias por aceptar , divertirse charlando :) </label>

  </div>
   </transition>
  <br>
        <input @click="handleClick" type="checkbox" id="check1" name="check1" value="true"> <br>
   <transition name="show">
      <button v-if=" !isPending && hideBtn">Iniciar sesión</button>
   </transition>

      <button v-if="isPending" disabled>Cargando</button>
   


  </form>
  </div>


</template>

<script>
import Chat from '../components/Chat.vue'
import getUser from '../composables/getUser'
import useDocument from '../composables/useDocument'
import useDocument2 from '../composables/useDocument2'
import getDocument from '../composables/getDocument'


import { ref } from 'vue'
import useLogin from  '../composables/useLogin'
import {useRouter} from 'vue-router'
export default {
    // emits:['chatDirection'],
    components: { Chat },
setup (props){

    const hideBtn = ref(false)
    const hidetxt = ref(true)
const { updateDoc} = useDocument('bam','b78dyTrFsSw8NH4X7tF9')
const { updateDocs} = useDocument2('bam','Z88rLYmZafHOcbQlcGWd')
    const {  document:ass } = getDocument('bam','Z88rLYmZafHOcbQlcGWd')

    const handleClick = ()=>{
        hideBtn.value =! hideBtn.value
        hidetxt.value =! hidetxt.value

    }
    const isPending = ref('')
    const email = ref('')
    const password  =ref('')
    const { error, login} = useLogin()
    const router = useRouter()
const {user} = getUser()

    const handleSubmit =  async ()  => {
        isPending.value = useLogin()
const loggy =ref(true)

        await login(email.value , password.value)
        if (!error.value){
            router.push({ name:'Chatroom2Es',params:{ id:loggy.value}})
            // console.log('user logged in')
 const newItem =  user.value.displayName
const alls0 = ass.value.alls.push(user.value.displayName)
const alls = ass.value.alls
             await updateDoc({
                allUsersIds2: newItem ,
                userLeft2: null
                //  items:[...props.item.items, newItem]
      

            })
              await updateDocs({
             alls:alls
             
             

            })
            // context.emit('logging')

        }
        else {
            isPending.value = false
        }
    }
    return { email , password , handleSubmit , error,  isPending , hideBtn , handleClick ,hidetxt }

}

}
</script>

<style scoped>
#nav{ color:red;display:block ; margin-top:0%; width:100% ;border-radius:0; background-color: white;position:relative;top:0px;}
.btn{font-family:monospace;font-size:12px;background:none; color:red;border-radius:10px;border-style:solid ;border-color:red; border-width:2px;box-shadow:2px 5px 5px rgba(0, 0, 0, 0.335)}

form{ background:url(../assets/bakkano1log.png) ;background-size:300% ;background-position: center;background-repeat: no-repeat;border-radius: 20px;z-index:1;background-color: white;
  width:280px;
margin:20px  auto; box-shadow: 3px 3px 10px red }
 
p{
     font-size: 25px;
  background: linear-gradient(rgb(255, 0, 0),rgb(201, 45, 45));
  background-clip: text;
  -webkit-text-fill-color:transparent;
}
 input { font-family: monospace;
     text-decoration: none;
  font-size: 17px;
  background: linear-gradient(rgb(248, 242, 242),rgba(255, 255, 255, 0.541)0.897), 255));
  background-clip: text;
  -webkit-text-fill-color:transparent;
  width: 70%;
  padding:10px;
  border-radius:20px;

  border: 2px groove rgb(255, 255, 255);
  outline:none;
  color:rgb(255, 255, 255);
  margin:10px auto;
}
label { font-family: monospace;
     text-decoration: none;
  font-size: 15px;
  background: linear-gradient(rgb(255, 255, 255),rgb(255, 255, 255));
  background-clip: text;
  -webkit-text-fill-color: transparent;
  max-width: 10px;
  outline:none;
  color:rgb(255, 255, 255);
}
 span{
  text-decoration:underline;
  font-weight: bolder;
  color:red;
  cursor:pointer
}

button{margin:20px auto;}


.show-enter-active{
  transition: all 0.5s ease;
}
.show-leave-active{
  transition: all 0s  step-end ;

}
.show-enter-from{transform:scaleY(0.3);opacity: 0;}
.show-leave-to{transform: scaleY(0.3);opacity:0}


</style>