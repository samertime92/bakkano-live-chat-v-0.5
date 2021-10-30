<template>
      <router-link id="nav" :to="{name:'Welcome'}"><button class="btn" >Exit</button></router-link>
  <transition name="show2">

  <h1 v-if="show"> Create menu Bakkano2 (EN)</h1>
  </transition >
  <transition name="show2">

<div v-if="show">
  <form @submit.prevent="handleSubmit">
  <input type="text" required placeholder="Category title" v-model="title">
  
  <label>Upload Category img</label>
  <div class="uplo">
      <h1>choose</h1>
  <input class="upload" type="file" required @change="handleChange">
  </div>
  <div class="error">{{fileError}}</div>
  <div class="error"></div>
  <button v-if="!isPending">Create</button>
  <button v-if="isPending" disabled>Loading...</button>

  </form>
</div>
  </transition >

<!--added -->

     <!-- <div v-if="error" class="error">Could not bring data</div> -->
   <div  id="eventContainer" v-if="documents">
          <div  v-for=" doc in formattedDocuments" :key="doc.id">
        <router-link class="links" :to="{name:'B2DeAdEN', params:{ id:doc.id}}">

              <div id="single">

              <!-- <div id="title"> 
                  {{doc.title}}
              </div> -->
              <div id="thumbnail">
            <img :src="doc.categoryURL" >
           
             </div>
             <div id="info">
                
                 {{doc.createdAt}}
                 <h3>by admin {{doc.userName}}</h3>
                  <h2>{{doc.title}}</h2>

             </div>

          </div>
        </router-link>

          </div>
        </div>
     <!-- ended -->
  
</template>

<script>
//added
import { formatDistanceToNow} from 'date-fns'
import { ref , computed, onUpdated } from 'vue'
import getCollections from '../composables/getCollections'

//



import menuStorage from  '../composables/menuStorage'
import useCollection from '../composables/useCollection'
import getUser from '../composables/getUser'
import { timestamp } from '../firebase/config'
export default {
setup(){
  const show = ref(false)
     const showw =()=>{

show.value=true

}


  
  setTimeout(showw, 0)
    const isPending =ref(false)
    const {filePath , url ,uploadImage} = menuStorage()
    const {user} = getUser()
    const title = ref('');
    const file = ref(null)
    const fileError = ref(null)
    const types = ['image/png','image/jpeg']
    const {addDoc, error} = useCollection('menuB2En')
    const handleChange= (e)=>{
       const selected = e.target.files[0]
       if (selected && types.includes(selected.type)){
           file.value = selected
           console.log(selected)
           fileError.value = null
       }
       else{
           file.value= null
           fileError.value = ' please select a valid image file (png or jpeg)'
       }
    }
    const handleSubmit = async()=>{
        if(file.value){
            isPending.value = true
            await uploadImage(file.value)
            await addDoc({
               title: title.value ,
               userId : user.value.uid,
               userName : user.value.displayName,
               categoryURL : url.value,
               filePath : filePath.value,
               items : [] ,
               createdAt : timestamp(),
               
            })
            isPending.value = false
            // if (!error.value){
                // console.log('playlist added')
            // }
            console.log(url.value,'image uploaded')
        }
   console.log(title.value)
    }
    //added
    const {  documents  } = getCollections('menuB2En')
    const formattedDocuments = computed(() => {
            if (documents.value){
                return documents.value.map( doc => {
                    let time = formatDistanceToNow(doc.createdAt.toDate())
                    return {...doc ,createdAt: time}
                })
            }

        })
        onUpdated(() => {
    documents.value.scrollTop = documents.value.scrollHeight
})

   


    return { show, user,title, handleSubmit, handleChange, fileError, isPending ,error , documents, formattedDocuments } 
         
     
    
}


}
</script>

<style scoped>

.delBtn{font-size:15px;position:absolute;margin:0 auto;z-index:0;padding:5px 10px}
#thumbnail{border-radius:100px!important;box-shadow:10px 5px 5px rgb(5, 5, 5) }
#single{background:linear-gradient(black,white,white,white,rgb(0, 0, 0))!important; border-radius: 100px!important;display:inline-block!important;box-shadow: 10px 5px 20px rgba(255, 255, 255, 0.568)!important;}
.show2-enter-active{
  transition: all 0.5s ease;
}
.show2-leave-active {
    transition: all 0.5s ease-in;
}
.show2-enter-from{transform:scale(0.5);opacity: 0;}
.show2-leave-to{transform: scale(0.3);opacity:0}
#nav{ color:red;display:block ; margin-top:0%; width:100% ;border-radius:0; background-color: rgb(255, 255, 255);position:relative;top:0px; padding-top:20px ;padding-bottom:20px }

.btn{font-family:monospace;:12px;background:none; color:red;border-radius:10px;border-style:solid ;border-color:red; border-width:2px;box-shadow:2px 5px 5px rgba(0, 0, 0, 0.335)}
.uplo h1{font-size: 30px; text-align: center;  background: -webkit-linear-gradient(rgb(134, 128, 128), #333); -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;}
.uplo{border:solid 2px;border-radius: 5px; width:200px;margin:5px auto;height:80px;background-color: rgba(255, 255, 255, 0.671);box-shadow:2px 4px  6px rgba(2, 53, 37, 0.9);margin: 20px auto;}
.upload{opacity: 0; position: absolute;width:200px;height:60px;top:430px;left:18%}

form{ height:350px;border-radius: 20px;;z-index:1;background:linear-gradient(180deg,rgba(255, 255, 255, 0.9),white,white,rgba(255, 255, 255, 0.671));box-shadow:2px 4px  30px rgba(255, 255, 255, 0.9);
border-color:rgb(255, 248, 248);border-style:solid;border-width:4px;;
  width:290px;
margin: 20px  auto;}
label {
    color: rgb(0, 0, 0);
  display: block;
  margin:20px 0 10px;
}
input { filter:in;margin:10px auto;box-shadow: 2px 5px 10px rgba(0, 0, 0, 0.418); ;
  width: 50%;
  padding:10px;
  border-radius:20px; border-style:none}

textarea { margin:10px auto;box-shadow: 2px 5px 10px rgba(0, 0, 0, 0.418);
  width: 50%;
  padding:10px;
  border-radius:20px;border-style:none}
h1{ filter: brightness(170%);
  font-size: 50px;
  background: linear-gradient(rgb(255, 255, 255), #333);
  background-clip: text;
 color: transparent;
}







/* added */

#eventContainer{display:grid; gap:1px;
grid-template-columns: 1fr;
}
.links{text-decoration: none;}
/* h1{ filter: brightness(170%); color: lightgray; */
  /* font-size: 25px;} */
h2{ filter: brightness(170%); text-decoration: none;
  font-size: 25px;
  background: linear-gradient(rgb(255, 255, 255), #333);
  background-clip: text;
 color: transparent;}
  h2{animation: change;transition: all ease;
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

#single{display:flex ;align-items: center; border-radius:10px;transform :scale(0.70);display:inline-block;
margin:5px auto;box-shadow: 20px 10px 20px rgba(221, 6, 6, 0.829);
transition: all ease 0.2s; background: linear-gradient(0deg, rgba(223, 5, 5, 0.979), rgba(88, 4, 84, 0.192), rgba(0, 0, 0, 0))}
#single:hover{transform :scale(1.1); box-shadow:
 1px 10px 20px rgba(255, 255, 255 ,0.5);transition: all ease 0.5s;filter:brightness(120%);border-radius:30px;background: linear-gradient(0deg, rgba(243, 239, 239, 0.979), rgba(88, 4, 84, 0.192), rgba(0, 0, 0, 0))}
 #thumbnail{max-width:100px; max-height:100px; overflow:hidden;border-radius:10px;}
img{max-width:150%;max-height:150; display:block}
#info{ margin:0 30px;}


/* ended */


</style>