<template>
   <div class="add-item">
     <div v-if="item">
<form @submit.prevent="handleSubmit">
<input type="text" required placeholder="item title" v-model="title">
<input type="text" required placeholder="description" v-model="desc">
<input type="text" required placeholder="price" v-model="price">
<input type="text" required placeholder="item allergens" v-model="allerg">
<button>Add</button>
</form>
</div>
</div>
</template>

<script>
import useDocument from '../composables/useDocument'
import { ref } from 'vue'
export default {
    props:['item'],
    setup(props){
            const { error5 , updateDoc } = useDocument('menuB2Es', props.item.id)
    const title = ref('')
    const desc = ref('')
    const price = ref('')
    const allerg = ref('')
    const handleSubmit = async ()  => {
        const newItem = {
            title:title.value,
            desc:desc.value,
            price:price.value,
            allerg:allerg.value,
            id: Math.floor(Math.random()*1000000)
        }
            console.log(newItem)
            await updateDoc({
                items:[...props.item.items, newItem]

            })
            title.value = '',
            desc.value = '' ,
            price.value = '',
            allerg.value = ''
                
            }
            return{ title , desc , price , allerg, handleSubmit, updateDoc , error5 }
    } 

}
</script>

<style scoped>
button{display: block; margin:40px auto;}
form{ height:350px;border-radius: 20px;;z-index:1;background:linear-gradient(180deg,rgba(209, 26, 26,0.9),rgba(107, 3, 3, 0.671));box-shadow:2px 4px  30px rgba(119, 53, 37, 0.9);
border-color:rgba(209, 26, 26,1);border-style:solid;border-width:4px;;
  width:290px;
margin: 20px  auto;}
label {
    color: seashell;
  display: block;
  margin:20px 0 10px;
}
input { filter:in;margin:10px auto;box-shadow: 2px 5px 10px rgba(0, 0, 0, 0.418); ;
  width: 50%;
  padding:10px;
  border-radius:20px; border-style:none}

textarea { margin:10px auto;
  width: 50%;
  padding:10px;
  border-radius:50px;}
h1{ filter: brightness(170%);
  font-size: 50px;
  background: linear-gradient(rgb(122, 10, 10), #333);
 background-clip: text;
 color: transparent;
}

</style> 