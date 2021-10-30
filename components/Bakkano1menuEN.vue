<template>
        <div v-if="error" class="error">Could not bring data</div>
   <div v-if="documents">
          <div v-for=" doc in formattedDocuments" :key="doc.id">
        <router-link class="links" :to="{name:'B1DetailsEN', params:{ id:doc.id}}">

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
</template>

<script>
import { formatDistanceToNow} from 'date-fns'

import { ref ,computed } from 'vue'
import getCollections from '../composables/getCollections'
export default {
    setup() {
    
    
    
    //   const  {user} = getUser()
  const { error, documents  } = getCollections('menuB1En')
    const formattedDocuments = computed(() => {
            if (documents.value){
                return documents.value.map( doc => {
                    let time = formatDistanceToNow(doc.createdAt.toDate())
                    return {...doc ,createdAt: time}
                })
            }

        })
      
  return {  error , documents,formattedDocuments  }
   
    }

}
</script>

<style scoped>

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
margin:0px auto;box-shadow: 1px 10px 20px rgba(255, 2, 2, 0.5);
transition: all ease 0.2s; background: linear-gradient(0deg, rgba(255, 0, 0, 0.979), rgba(88, 4, 84, 0.192), rgba(0, 0, 0, 0))}
#single:hover{transform :scale(0.9); box-shadow:
 1px 10px 20px rgba(255, 255, 255, 0.904);transition: all ease 0.5s;filter:brightness(120%);border-radius:30px;background: linear-gradient(0deg, rgba(243, 239, 239, 0.979), rgba(88, 4, 84, 0.192), rgba(0, 0, 0, 0))}
 #thumbnail{max-width:100px; max-height:100px; overflow:hidden;border-radius:10px;}
img{max-width:150%;max-height:150; display:block}
#info{ margin:0 30px;}

</style>