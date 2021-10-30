<template>
     <form @sumbit.prevent="handleSubmit">
         <input type="email" placeholder="email please" v-model="fuck">
         <input type="password" placeholder="password" v-model="you ass">
         <button>login</button>
     </form>
</template>

<script>
import uselogin from '@/
export default {
    setup(){
        const {error, login} = useLogin()

const email = ref('')
const password = ref('')

const handlesubmit = async () =>{
    const res = await login(emial.value , password.value)
if(!error.value){
    console.log('user logged in')
}
}

return { email ,password}

    }

}
</script>

<style>

</style>