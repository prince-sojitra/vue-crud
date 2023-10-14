<script setup>
import {reactive} from 'vue'
import axios from 'axios'
let Login = reactive({
    "uname" : null,
    "password" : null
})
async function dataCheck(){
    let res = await axios.post('http://13.51.56.32:3001/user/login/',Login)
    console.log(res);
}
function SubmitData(){
    dataCheck()
    Login.uname = null
    Login.password = null
}
</script>

<template>      
    <h1>Login page</h1>
    <form @submit.prevent="SubmitData">
        <input type="text" placeholder="uname" v-model="Login.uname"><br>
        <input type="password" placeholder="password" v-model="Login.password"><br>
        <input type="submit">
    </form>
</template>

<style scoped>

</style>
