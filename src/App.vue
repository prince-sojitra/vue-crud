<script setup>
import {ref} from 'vue'
console.log();
let token = ref(localStorage.getItem('token'))
</script>

<template>
    <router-link to="/">Home</router-link> &nbsp;&nbsp;&nbsp;
    <router-link to="/signup">signup</router-link> &nbsp;&nbsp;&nbsp;
    <router-link to="/login">login</router-link> &nbsp;&nbsp;&nbsp;
    <router-link to="/contact" v-if="token">contact</router-link> &nbsp;&nbsp;&nbsp;
    <router-view></router-view>
</template>

<style scoped>

</style>
