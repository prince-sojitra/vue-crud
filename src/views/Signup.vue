<script setup>
import { reactive } from 'vue';
import axios from 'axios'

let Signup = reactive(
    {
        "fname": null,
        "lname": null,
        "uname": null,
        "password": null,
        "contact": null,
        "email": null
    }
)
async function Submit() {
    let res = await axios.post('http://13.51.56.32:3001/user/signup/',Signup) 
    console.log();
    localStorage.setItem('token',res.data.token)
}
function SubmitData() {
    Submit()
    console.log('hello');
    
    Signup.fname = null
    Signup.lname = null
    Signup.uname = null
    Signup.password = null
    Signup.contact = null
    Signup.email = null
}
</script>

<template>
    <h1>Signup page</h1>
    <form @submit.prevent="SubmitData">
        <input type="text" placeholder="fname" v-model="Signup.fname"><br>
        <input type="text" placeholder="lname" v-model="Signup.lname"><br>
        <input type="text" placeholder="uname" v-model="Signup.uname"><br>
        <input type="password" placeholder="password" v-model="Signup.password"><br>
        <input type="number" placeholder="contact" v-model="Signup.contact"><br>
        <input type="email" placeholder="email" v-model="Signup.email"><br>
        <input type="submit">
    </form>
</template>

<style scoped></style>
