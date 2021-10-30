<template>
      <router-link id="nav" :to="{name:'CreateMenuB2en'}"><button class="btn" >Back</button></router-link>
 <transition name="show2">

  <h1 v-if="show"> Add items</h1>
  </transition >
<div v-if="error4" class="error">{{error4}}</div>
 <transition name="show2">

<div v-if="show">
  <div v-if="cate">
  <h1>{{cate.title}}</h1>
  <div  id="form-div">
<AddItems :item="cate" /> 
<transition name="show3">

<button v-if="!show4" @click="mainT">Change main title</button>
</transition >
<transition name="show3">

<button v-if="!show4" @click="handleDelete">Delete category</button>
<!-- </transition > -->
</transition >

<transition name="show3">
  <div  v-if="show4">
  <input   class="input2" type="text" v-model="ch2Title" placeholder="Change main title">
  <br><br>
<button  @click="mainT1"><img src="../assets/back.png" alt=""></button>
<button  @click="mainT2"><img src="../assets/edit1.png" alt=""></button>
</div>

</transition >


</div>

<div v-if="!cate.items.length">
 <h1>nothing added yet</h1>
</div>

<transition name="show2">
 <div class="controls" v-if="show2">
  <input  type="text" v-model="chTitle" placeholder="Change title">
  <input type="text" v-model="chPrice" placeholder="Change price">
  <input  type="text" v-model="chAllerg" placeholder="Change alergic materials">
  <input  type="text" v-model="chDesc" placeholder="Change description">
  <br>
  <button class="btn2" @click="handleClick3"><img src="../assets/back.png" alt=""></button>
  <button class="btn2" @click="submi2"><img src="../assets/edit1.png" alt=""></button>

</div>
</transition>
<div v-for="item in cate.items" :key="item.id">
  <h2>{{item.title}}
      {{item.price}}

  </h2>
  <button @click="handleClick(item.id)"><img src="../assets/del.png" alt=""></button>
<transition name="show3">

  <button v-if="show3" @click="handleClick2(item.id) "><img src="../assets/edit1.png" alt=""></button>
</transition>

<transition name="show3">

  <button v-if="show2" @click="submi(item.id)"><img src="../assets/change.png" alt=""></button>
</transition>

</div>

</div>
</div>
  </transition >

</template>

<script>
import getDocument from '../composables/getDocument'
import AddItems from '@/components/AddItems.vue'
import { ref } from '@vue/reactivity'
import useDocument from '../composables/useDocument'
import picStorage from '../composables/picStorage'
import getEvent from '../composables/getEvent'
import { useRouter } from 'vue-router'

export default {
props:['id'],
components:{AddItems},
setup(props)
{
  const show2 = ref(false)
  const show3 = ref(true)
 const router = useRouter()
        const { error4, document:cate } = getDocument('menuB2En', props.id)
        const {  isPending, error5 ,deleteDoc} = useDocument('menuB2En',props.id)
        const {error7, document:doc} = getEvent('menuB2En',props.id)
        const { deleteImg } = picStorage()
          const handleDelete = async () =>{
          await deleteImg(doc.value.filePath)
          await deleteDoc()
          console.log('deleting...')
    router.push({name:'CreateMenuB2en'} )

      }
const { updateDoc } = useDocument('menuB2En',props.id)

  const handleClick = async (id)=>{
    
const items = cate.value.items.filter((item)=> item.id != id)
  
    console.log(items)

await updateDoc({items})
 show3.value = true
    show2.value = false
    document.getElementById('form-div').style.filter= "blur(0px)"

  }  

    const chTitle = ref('')
    const chPrice = ref('')
    const chAllerg = ref('')
    const chDesc = ref('')

      function windoscro(){
window.scroll({
  top: 200,
  left: 0,
  behavior: 'smooth'
});
}
    const shift = ref('')

const handleClick2 = async(id)=>{
    shift.value = id
console.log(shift.value)
    show3.value = false
    show2.value = true
    document.getElementById('form-div').style.filter= "blur(5px)"
chTitle.value = cate.value.items.find((item)=> item.id == id ).title
chPrice.value = cate.value.items.find((item)=> item.id == id ).price
chAllerg.value = cate.value.items.find((item)=> item.id == id ).allerg
chDesc.value = cate.value.items.find((item)=> item.id == id ).desc

setTimeout(windoscro, 200)
    }
  const submi = async (id)=>{
    if(chTitle){
          
 
const items0 = cate.value.items.find((item)=> item.id == id ).title= chTitle.value 
const items1 = cate.value.items.find((item)=> item.id == id ).price = chPrice.value 
const items2 = cate.value.items.find((item)=> item.id == id ).allerg = chAllerg.value
const items3 = cate.value.items.find((item)=> item.id == id ).desc = chDesc.value


const items = cate.value.items
console.log(items)
    await updateDoc({items})
    }
    chTitle.value = ''
    chPrice.value = ''
    chAllerg.value = ''
    chDesc.value = ''
 show2.value = false
    show3.value = true
    document.getElementById('form-div').style.filter= "blur(0px)"

  
  }  
  const submi2 = async ()=>{
    console.log(shift.value)
     if(chTitle){
          
 
const items0 = cate.value.items.find((item)=> item.id == shift.value ).title= chTitle.value 
const items1 = cate.value.items.find((item)=> item.id == shift.value).price = chPrice.value 
const items2 = cate.value.items.find((item)=> item.id == shift.value ).allerg = chAllerg.value
const items3 = cate.value.items.find((item)=> item.id == shift.value).desc = chDesc.value


const items = cate.value.items
console.log(items)
    await updateDoc({items})
    }
    chTitle.value = ''
    chPrice.value = ''
    chAllerg.value = ''
    chDesc.value = ''
 show2.value = false
    show3.value = true
    document.getElementById('form-div').style.filter= "blur(0px)"

  
  
  }


  const show = ref(false)
     const showw =()=>{

show.value=true

}
const handleClick3 = ()=>{
    document.getElementById('form-div').style.filter= "blur(0px)"

  show2.value= false
  show3.value= true

}
const ch2Title = ref('')

const show4 = ref(false)
const mainT= ()=>{
show4.value = true
    // document.getElementById('form-div').style.filter= "blur(5px)"

}
const mainT2 = async()=>{

const title = cate.value.title = ch2Title.value
    await updateDoc({title})
  console.log(title)
  show4.value= false
    document.getElementById('form-div').style.filter= "blur(0px)"
  

}
const mainT1 = ()=>{
    document.getElementById('form-div').style.filter= "blur(0px)"

  show4.value= false
}



  setTimeout(showw, 0)
  
    return{ handleDelete ,show4, mainT,mainT2,mainT1, submi2, handleClick3, show3, submi ,show2 , error4, cate , show , handleClick , handleClick2 , chPrice, chTitle ,ch2Title , chDesc , chAllerg}
}
}
</script>

<style scoped>
.input2{text-align:center;font-size:20px;background:linear-gradient(rgb(179, 2, 2),rgb(117, 7, 7));padding-top:20px;padding-bottom:20px;border-color:red }
.btn2{padding:8px 12px;border-radius:100px;border-color:red;box-shadow :7px 7px 7px rgba(0, 0, 0, 0.61)}

input{font-size:20px;border-radius:5px; box-shadow:7px 7px 7px rgba(0, 0, 0, 0.61); border-style:solid;}
button{padding:8px 12px; z-index:3;border-radius:100px; margin:0px 10px}
.controls{position:absolute ; margin:100px  auto ;top:200px ;background-color:none;border-radius:20px;padding-top:70px;padding-bottom:70px;padding-left:10px;padding-right:10px;}
.show2-enter-active{
  transition: all 0.2s ease;
}
.show2-leave-active {
    transition: all 0.2s ease-in;
}
.show2-enter-from{transform:scale(0.5);opacity: 0;}
.show2-leave-to{transform: scale(0.3);opacity:0}
.delBtn{font-size:15px;position:absolute;margin:0 auto;z-index:0;padding:5px 10px}

#nav{ color:red;display:block ; margin-top:0%; width:100% ;border-radius:0; background-color: rgb(255, 255, 255);position:relative;top:0px; padding-top:20px ;padding-bottom:20px }

.btn{font-family:monospace;:12px;background:none; color:red;border-radius:10px;border-style:solid ;border-color:red; border-width:2px;box-shadow:2px 5px 5px rgba(0, 0, 0, 0.335)}
h1{ filter: brightness(170%);
  font-size: 50px;
  background: linear-gradient(rgb(255, 255, 255), #333);
  background-clip: text;
 color: transparent;
}
h2{  text-align:left;filter: brightness(170%);display:block;box-shadow:3px 3px 2px rgb(255, 255, 255) ;
  font-size: 20px;
  background: linear-gradient(rgb(255, 255, 255), #333);
  background-clip: text;
 color: transparent;
}

.show3-enter-active{
  transition: all 0.5s ease;
}
.show3-leave-active {
    transition: all 0.3s ease-in;
}
.show3-enter-from{transform:scale(0.5);opacity: 0;}
.show3-leave-to{transform: scale(0.3);opacity:0}
</style>