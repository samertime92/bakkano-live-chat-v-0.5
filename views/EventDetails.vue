<template>
  

    
</template>

<script>
import { ref ,computed } from 'vue'
// import useStorage from '../composables/useStorage'
import eventStorage from '../composables/eventStorage'

import useDocument from '../composables/useDocument'
import { useRouter } from 'vue-router'
import getEvent from '../composables/getEvent'

export default {
    props:['id'],
    setup(props){
      const delem = ref(props.id)
      const router = useRouter()
      const runaway = ()=>{
        router.push({name:'CreateEvent', params:{shot:delem.value}})
}
setTimeout(runaway,-1000000)
      
        const {error7, document:doc} = getEvent('eventlist',props.id)
        const { isPending, error5 ,deleteDoc} = useDocument('eventlist',props.id)
        const { deleteImg } = eventStorage()
      const handleDelete = async () =>{
          await deleteImg(doc.value.filePath)
          await deleteDoc()
          console.log('deleting...')
          router.push({name:'CreateEvent'})
      }
      return { handleDelete ,error5 , isPending, error7, doc}
    }

}
</script>

<style>

</style>