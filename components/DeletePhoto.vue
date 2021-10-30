<template>
   <div class="navbar1">
          <div class="div1"><h1 @click="handleMenu3" class="links"> Reserve</h1></div>

        <div class="div2"> <h1  @click ="handleClick" class="links"> <div class="links4">Logout</div> </h1></div> 
          <div class="div3"><h1   @click ="handleMenu2"  class="links">Chatrooms</h1></div>



      
        </div>
</template>

<script>
import useDocument from '../composables/useDocument'
import picStorage from '../composables/picStorage'
import getEvent from '../composables/getEvent'
import { useRouter } from 'vue-router'
import { ref } from '@vue/reactivity'

export default {

    props:['id'],
setup(props)
{
    const delem =ref(props.id)
    const router = useRouter()
    console.log(delem.value)
const runaway=()=>{
    router.push({name:'Account', params:{shot:delem.value}})
}
setTimeout(runaway,-1000000)
        const {  isPending, error5 ,deleteDoc} = useDocument('userPhoto',props.id)
        const { deleteImg } = picStorage()
        const {error7, document:doc} = getEvent('userPhoto',props.id)

  const handleDelete = async () =>{
          await deleteImg(doc.value.filePath)
          await deleteDoc()
          console.log('deleting...')
      }
      return {handleDelete}
}
}
</script>

<style scoped>
h1{font-size:15px}
.navbar1{ display:grid;grid-template-columns: 1fr 1fr 1fr ; gap:10%;
/* grid-template-rows: 2fr 1fr; */
/* background-position: center;background-size: 20px; */
  ;background:rgb(255, 255, 255);border-radius:0px;  padding:20px 25px;margin-bottom:50px
;}
/* .uImg{max-width: 100px; border-radius: 50px;} */
.submit{display:block ;background-color:rgb(255, 0, 0);z-index: 3;margin:10px auto }
.loading{ display:block; background-color:rgb(0, 4, 255);z-index: 3; margin:10px auto}

#userImg{z-index:3; border-style:none; border-radius:20px;color:red ;background:linear-gradient(white ,white ,black);opacity:0%;width:100%;height:30px;position: relative;; }
#userImgDiv{position: relative;;border-style: solid; border-radius:50px;max-width:1000px;overflow:hidden;width:100px;background-color: red;height:100px;;z-index: 3;}
.img1{width:15%;position: relative;left:0px; margin:0px;}
.img2{width:15%;position: relative;left:10px;margin:0px;}

.navbar{padding:1px 10px;margin-bottom:60px;background:white;border-radius:20px;
;}
.links2{ transform:skewY(0deg);background:linear-gradient(0deg,white,white,white,white,white,white,white,white,white,rgba(255, 255, 255, 0.219));box-shadow:3px 10px 20px rgba(255, 255, 255, 0.5);font-weight:bolder;font-size:15px;color:red;text-decoration:none;font-family: monospace;border:1px;border-radius: 10px;border-color:rgb(245, 143, 143);border-style:none;padding: 5px;border-width:1px; }
.links2:hover{background-color:rgb(0, 0, 0);color:rgb(0, 0, 0);transition: 0.5s;transform:scale(1.2);box-shadow:3px 10px 10px rgba(255, 255, 255, 0.8)}
.links{background-color:none;font-weight:bolder;font-size:15px;color:rgb(255, 38, 38);text-decoration:none;font-family: monospace;border:2px;border-radius: 10px;border-color:rgba(255, 0, 0, 0.26);border-style: solid;padding: 5px;    box-shadow: 2px 10px 10px rgb(24 24 24 / 35%); }
.links:hover{ border-width:2px;border-color:rgb(255, 0, 0);background:rgb(255, 0, 0);color:rgb(255, 255, 255);transition: 0.5s;}
.div0{background:linear-gradient(black, white ,white ,white);display:inline-block;border-radius:20px;margin:20px auto ; width:30%;height:40px;box-shadow:2px 3px 10px rgba(255, 255, 255, 0.452);}
</style>