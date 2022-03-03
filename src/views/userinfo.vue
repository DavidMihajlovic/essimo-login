<template>
    <div>
        <div class="border">
            <span class="bschr">ID:</span><span class="obj">{{id}}</span>
        </div>

        <div class="border">
            <span class="bschr">Name:</span><span class="obj">{{name}}</span>
        </div>
        <div class="border">
            <span class="bschr">Email:</span><span class="obj">{{email}}</span>
        </div>
        
        <a href="http://localhost:8080/login"><button id="out" class="logout btn btn-warning" @click="sendData">Logout</button></a>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'userinfo',
    data(){
        return {
            id:0,
            name:"",
            email:"",

        }
    },
    mounted(){
        let token = localStorage.getItem("Token");
        console.log(token);
        axios.defaults.headers.common = {
        'Authorization': 'Bearer ' + token
        };

        axios.get("https://api.essimo.io/api/v1/auth/user")
                .then((response)=>{
                    console.log(response);
                    this.id = response.data.id;
                    this.name = response.data.name;
                    this.email = response.data.email
                });

    },
    methods:{
        sendData(){
            axios.post("https://api.essimo.io/api/v1/auth/logout", {})
                .then((response)=>{
                    localStorage.setItem('Token', response.data.access_token);
                    console.log("Erflogreich");
                });
        },
    }
}
</script>


<style>
.border{
    border: 1px solid darkgray;
    width: 20rem;
    height: 2rem;
    margin-bottom: 1rem;
    margin-left: auto;
    margin-right: auto;
    background-color: rgb(236, 236, 236);
}
.bschr{
    float: left;
    padding-left:1rem;
    margin-top:0.5rem;
}
.obj{
    float: right;
    padding-right:1rem;
    margin-top:0.5rem;
}
.logout {
    width: 20rem;
    height: 3rem;
    /* border: 1px solid rgb(255, 200, 47);
    background-color: rgb(255, 200, 47); */
    color: rgb(12, 39, 12);
    cursor: pointer;
    font-size: 1.5em;
    border-radius: 20mm;
}
#out{
    border-radius: 20mm;
}
</style>