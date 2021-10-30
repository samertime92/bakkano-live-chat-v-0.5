<template>
<img  @click="scrollMe" id="arrow" src="../assets/arrow.png" alt="">
<img  @click="scrollMe2" id="arrow3" src="../assets/arrow.png" alt="">

<div class="navbar1">

          <!-- <h1><router-link class="links" :to="{ name: 'Chatroom'}">Chatroom</router-link></h1> -->
         <div class="div1"> <h4><router-link class="links" :to="{ name: ''}">Reserve</router-link></h4></div>
        <div class="div2">  <h4><router-link class="links" :to="{ name: 'Welcome'}">Home</router-link></h4></div>

        <div class="div3">  <h4><router-link class="links" :to="{ name: ''}">Community</router-link></h4></div>

<!-- <router-link class="links" :to="{ name: 'Menu'}"</router-link> -->


      
  </div>
<div v-if="error4" class="error">{{error4}}</div>

  <div id="caty" v-if="cate">
<h1>{{cate.title}}</h1>
<div v-if="!cate.items.length">
 <h1>nothing added yet</h1>
</div>
<div class="itemholder">

<div  v-for="item in cate.items" :key="item.id">
  <div  class="item">
  <h2>{{item.title}} {{item.price}}</h2>

  <h3> {{item.desc}}</h3>
  <h4>{{item.allerg}}</h4>
  </div>
</div>
</div>
</div>



 



 
 



 <div>
     


 <div v-if="documents">
          <div  v-for=" doc in formattedDocuments" :key="doc.id">
        <router-link class="links"  :to="{name:'Mirrorb2EN', params: {id:doc.id} } ">

              <div id="single">
              <!-- <div id="title"> 
                  {{doc.title}}
              </div> -->
              <div id="thumbnail">
            <img :src="doc.categoryURL" >
           
             </div>
             <div id="info">
                
                  <h1>{{doc.title}}</h1>

             </div>
            

          </div>
        </router-link>

          </div>




 </div>
 </div>


</template>

<script>
import { roundToNearestMinutes } from "date-fns/esm/fp"



import { useRouter } from "vue-router"
import { useRoute } from 'vue-router'


import { formatDistanceToNow} from 'date-fns'

import { ref ,computed,watch } from 'vue'
import getCollections from '../composables/getCollections'
import Bakkano2menuEN from '../components/Bakkano2menuEN.vue'





import getDocument from '../composables/getDocument'
import AddItems from '@/components/AddItems.vue'

export default {
props:['id'],
components:{AddItems,Bakkano2menuEN},
setup(props,context){

  
const scrollMe = () =>{
   document.getElementById('arrow').style.width="8%";
   document.getElementById('arrow').style.opacity="20%";

   document.getElementById('arrow3').style.width="10%";
   document.getElementById('arrow3').style.opacity="50%";


  window.scroll({
    top: 20000,
  left: 0,
  behavior: 'smooth'
})
};
const scrollMe2 = () =>{
   document.getElementById('arrow').style.width="10%";
   document.getElementById('arrow').style.opacity="50%";

   document.getElementById('arrow3').style.width="8%";
   document.getElementById('arrow3').style.opacity="20%";

   
  
  window.scroll({
    top: 0,
  left: 0,
  behavior: 'smooth'
})
};

 const route = useRoute()
const router = useRouter()
console.log(route)


    const { error4, document:cate  } = getDocument('menuB2En', route.params.id)


// watch('$route.params.id' , (id) => {

// })


   

// let data = await fetch('http://B2DetailsEN/:id')
// }
// load()
//    })
// const userData = ref()



// const refresh = () => {
//       route.params.id,
//       async newId => {
//         userData.value = await fetchUser(newId)}
// }
 
    //   const  {user} = getUser()
  const { error, documents  } = getCollections('menuB2En')
    const formattedDocuments = computed(() => {
            if (documents.value){
                return documents.value.map( doc => {
                    let time = formatDistanceToNow(doc.createdAt.toDate())
                    return {...doc ,createdAt: time}
                })
            }


        })
    



    return{ error4 ,cate, error , documents, formattedDocuments , scrollMe , scrollMe2  }
}
}
</script>

<style  scoped>

#caty{transition:1s}
#arrow{ transition :0.5s; top:250px; right:0px;position: fixed; width:10% ; opacity:50%;z-index:0;background:none; margin:0 10px; padding: 0px auto;}
#arrow3{ transform:rotate(180deg);transition :0.5s; top:300px; right:0px;position: fixed; width:10% ; opacity:20%;z-index:0;background:none; margin:0 10px; padding: 0px auto;}
.navbar1{ display:grid;grid-template-columns: 1fr 1fr 1fr ; gap:10%;
/* grid-template-rows: 2fr 1fr; */
/* background-position: center;background-size: 20px; */
  ;background:rgb(255, 255, 255);border-radius:0px;  padding:20px 25px;margin-bottom:50px
;}

.links2{ transform:skewY(0deg);background:linear-gradient(0deg,white,white,white,white,white,white,white,white,white,rgba(255, 255, 255, 0.219));box-shadow:3px 10px 20px rgba(255, 255, 255, 0.5);font-weight:bolder;font-size:15px;color:red;text-decoration:none;font-family: monospace;border:1px;border-radius: 10px;border-color:rgb(245, 143, 143);border-style:none;padding: 5px;border-width:1px; }
.links2:hover{background-color:rgb(255, 255, 255);color:rgb(0, 0, 0);transition: 0.5s;transform:scale(1.2);box-shadow:3px 10px 10px rgba(255, 255, 255, 0.8)}


.links{background-color:none;font-weight:bolder;font-size:15px;color:rgb(255, 38, 38);text-decoration:none;font-family: monospace;border:2px;border-radius: 10px;border-color:rgba(255, 0, 0, 0.26);border-style: solid;padding: 5px;box-shadow:2px 4px  6px rgba(47,79,79,0.5) }
.links:hover{ border-width:2px;border-color:rgb(255, 0, 0);background:rgb(255, 0, 0);color:rgb(255, 255, 255);transition: 0.5s;}

h4{color:white ; display:inline-block;background-color:none;border-radius:20px; box-shadow: 2px 10px 10px rgba(85, 83, 83,0.350)}
.itemholder{background:white;border-radius: 0px;box-shadow: 2px 5px 20px rgb(255, 255, 255);margin-bottom:30%;}
.item{;display: block; border-radius: 0px; box-shadow: 1px 10px 20px rgba(255, 255, 255 ,0.5);
background-color: red;align-content:center;background: linear-gradient(0deg, rgba(243, 239, 239, 0.5), rgba(88, 4, 84, 0.1), rgba(0, 0, 0, 0))}
.links{text-decoration: none;}
/* h1{ filter: brightness(170%); color: lightgray; */
  /* font-size: 25px;} */
h1{ filter: brightness(170%); text-decoration: none;
  font-size: 35px;
  background: -webkit-linear-gradient(rgb(22, 22, 22), rgb(248, 242, 242));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;}
  h1{animation: change;transition: all ease;
      animation-fill-mode: forwards;
      animation-iteration-count: infinite;
      animation-duration: 6s;
      animation-timing-function: ease-in-out;}
 @keyframes change {
    0%{opacity: 1;}
    50%{opacity: 0.3;}
    100%{opacity: 1;}
 }
 h3{color:rgba(77, 75, 75, 0.972);font-size: 15px;}

#single{display:flex ;align-items: center; border-radius:50px;transform :scale(0.75);
margin:0px auto;box-shadow: 1px 10px 20px rgba(255, 255, 255 ,0.5);
transition: all ease 0.2s; background: linear-gradient(0deg, rgba(243, 239, 239, 0.979), rgba(122, 119, 122, 0.192), rgba(0, 0, 0, 0))}
#single:hover{transform :scale(0.9); box-shadow:
 1px 10px 20px rgba(255, 255, 255, 0.904);transition: all ease 0.5s;filter:brightness(120%);border-radius:30px;background: linear-gradient(0deg, rgba(243, 239, 239, 0.979), rgba(88, 4, 84, 0.192), rgba(0, 0, 0, 0))}
 #thumbnail{max-width:100px; max-height:100px; overflow:hidden;border-radius:10px;}
img{max-width:150%;max-height:150; display:block}
#info{ margin:0 30px;}
h2{ filter: brightness(170%);
  font-size: 20px;
  background: -webkit-linear-gradient(rgb(0, 0, 0), rgba(44, 43, 43, 0.719));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;}
</style>