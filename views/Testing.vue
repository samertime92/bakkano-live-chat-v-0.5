<template>
        <div v-if="error" class="error">Could not bring data</div>

   <div v-if="documents">
          <div v-for=" doc in documents" :key="doc.id">
            {{doc.eventURl}} 
          </div>
        </div>
</template>

<script>
import getCollections from '../composables/getCollections'
export default {
    setup(){
      const  {user} = getUser()
  const { error, documents } = getCollections('eventlist')
  return {  error , documents }

    }

}
</script>

<style>

</style>