<template>
        <div v-if="error" class="error">Could not bring data</div>
   <div v-if="documents">
          <div v-for=" doc in formattedDocuments" :key="doc.id">
        <router-link class="links" :to="{name:'EventDetails', params:{ id:doc.id}}">

              <div id="single">
              <!-- <div id="title"> 
                  {{doc.title}}
              </div> -->
              <div id="thumbnail">
            <img :src="doc.eventURL" >
           
             </div>
             <div id="info">
                <h3>{{doc.description}} </h3> 
                
                 {{doc.createdAt}}
                 <h3>by admin {{doc.userName}}</h3>
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
  const { error, documents  } = getCollections('eventlist')
    const formattedDocuments = computed(() => {
            if (documents.value){
                return documents.value.map( doc => {
                    let time = formatDistanceToNow(doc.createdAt.toDate())
                    return {...doc ,createdAt: time}
                })
            }

        })
      
  return {  error , documents, formattedDocuments  }
   
    }

}
</script>

<style scoped>
.links{text-decoration: none;}
/* h1{ filter: brightness(170%); color: lightgray; */
  /* font-size: 25px;} */
h1{ filter: brightness(170%); text-decoration: none;
  font-size: 25px;
  background: -webkit-linear-gradient(rgb(255, 255, 255), #333);
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

#single{display:flex ;align-items: center; border-radius:10px;transform :scale(0.95);animation:colorize2 4s infinite ease-out alternate-reverse, running;
margin:30px auto;box-shadow: 20px 10px 20px rgba(221, 6, 6, 0.829);
transition: all ease 0.2s; background: linear-gradient(0deg, rgba(223, 5, 5, 0.979), rgba(88, 4, 84, 0.192), rgba(0, 0, 0, 0))}
#single:hover{animation: paused;transform :scale(1.1); box-shadow:
 1px 10px 20px rgba(255, 255, 255 ,0.5);transition: all ease 0.5s;filter:brightness(120%);border-radius:30px;background: linear-gradient(0deg, rgba(243, 239, 239, 0.979), rgba(88, 4, 84, 0.192), rgba(0, 0, 0, 0))}
 #thumbnail{transition:ease 0.5s;max-width:100px; max-height:100px; overflow:hidden;border-radius:10px;box-shadow:7px 7px 2px rgb(109, 0, 0);}
img{max-width:150%;max-height:150; display:block,}
#info{ margin:0 30px;}
#thumbnail:hover{transform:scale(1.2)skew(5deg) ; animation:paused; box-shadow:7px 4px 1px rgba(255, 252, 252, 0.514);

}
#thumbnail{animation:colorize 1s infinite ease forwards running}
@keyframes colorize{
  0%{box-shadow:7px 7px 2px rgb(109, 0, 0);}
  5%{box-shadow:7px 4px 1px rgb(255, 252, 252)}
  10%{box-shadow:7px 7px 2px rgb(109, 0, 0);}

  100%{box-shadow:7px 7px 2px rgb(109, 0, 0);}
}
@keyframes colorize2{
0%{box-shadow: 20px 10px 20px rgba(221, 6, 6, 0.829);}
25%{box-shadow: 10px 10px 20px rgba(221, 6, 6, 0.829);}
50%{box-shadow: -10px 5px 20px rgba(221, 6, 6, 0.829);}
75%{box-shadow: -20px 0px 20px rgba(221, 6, 6, 0.829);}
100%{box-shadow: -20px -10px 20px rgba(221, 6, 6, 0.829);}
}

</style>