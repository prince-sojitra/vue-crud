<script setup>
import { reactive, onMounted, ref } from 'vue'
import axios from 'axios'
let contact = reactive({
    "fname": null,
    "lname": null,
    "contact": null,
    "city": null,
    "country": null
})
let EditID = ref(null)
let allData = ref([])

const getData = async () => {
    let res = await axios.get('http://13.51.56.32:3001/phonebook/findbyuser', {
        headers: {
            usertoken: localStorage.getItem('token')
        }
    })
    console.log(res.data.data);
    allData.value = res.data.data
}

onMounted(async () => {
    getData()
})

async function DeleteData(id) {
    console.log();
    let res = await axios.delete('http://13.51.56.32:3001/phonebook/delete?id=' + id, {
        headers: {
            usertoken: localStorage.getItem('token')
        }
    })
    getData()
}

async function DataSubmit() {
    if (EditID.value != null) {
        let res = await axios.patch('http://13.51.56.32:3001/phonebook/update?id='+EditID.value,contact,{
            headers: {
                usertoken: localStorage.getItem('token')
            }
        })
    } else {
        let res = await axios.post('http://13.51.56.32:3001/phonebook/create/', contact, {
            headers: {
                usertoken: localStorage.getItem('token')
            }
        })
    }

    getData()
}


async function EditData(id) {

    let dataEdit = allData.value[id]
    contact.fname = dataEdit.fname
    contact.lname = dataEdit.lname
    contact.contact = dataEdit.contact
    contact.city = dataEdit.city
    contact.country = dataEdit.country
    EditID.value = dataEdit._id

}



function SubmitData() {
    DataSubmit()
    contact.fname = null
    contact.lname = null
    contact.contact = null
    contact.city = null
    contact.country = null
}
</script>

<template>
    <h1>Contact page</h1>
    <form @submit.prevent="SubmitData">
        <input type="text" placeholder="fname" v-model="contact.fname"><br>
        <input type="text" placeholder="lname" v-model="contact.lname"><br>
        <input type="text" placeholder="contact" v-model="contact.contact"><br>
        <input type="text" placeholder="city" v-model="contact.city"><br>
        <input type="text" placeholder="country" v-model="contact.country"><br>
        <input type="submit">
    </form>

    <table border="1" width="100%">
        <tr>
            <th>fname</th>
            <th>lname</th>
            <th>contact</th>
            <th>city</th>
            <th>delete</th>
            <th>Edit</th>
        </tr>
        <tr v-for="(data, i) in allData" :key="data._id">
            <td> {{ data.fname }} </td>
            <td> {{ data.lname }} </td>
            <td> {{ data.contact }} </td>
            <td> {{ data.city }} </td>
            <td><button @click="DeleteData(data._id)">Delete</button></td>
            <td><button @click="EditData(i)">Edit</button></td>
        </tr>
    </table>
</template>

<style scoped></style>
