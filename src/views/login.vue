<template>

    <div class="log">
        <img  class="mb-4" alt="Vue logo" src="../assets/logo.png">
        <form>
            <div class="login">
                <div class=" form-group">
                <input v-model="email" type="text" placeholder="Email eingeben">
                <span class="iconeye fa-regular fa-eye" v-on:click="ShowHidePW" style="cursor: pointer">
            
                </span>
                <input v-model="password" id="pw" type="password" placeholder="Passwort eingeben"> 
                </div>
                </div>
                </form>
                <div class="btns">
                <button class=" btn btn-success" id="fstbtn" @click="sendData()">Login</button>
                <a href="http://localhost:8080/register"><button class=" btn btn-warning" id="scndbtn">Register</button></a>
                
                </div>
                
            </div>
        
    
</template>




<script>
import $ from'jquery'
import axios from 'axios'


export default {
    name:'login',
    data(){
        return {
            email:"",
            password:"",
            

        }
    },
    methods:{
        ShowHidePW(){  
                $('.iconeye').toggleClass("fa-eye fa-eye-slash");

                if ($('#pw').attr("type") == "password") {
                    $('#pw').attr("type", "text");
                } else {
                    $('#pw').attr("type", "password");
                }         
        },
        sendData(){
            console.log("Test");
            axios.post("https://api.essimo.io/api/v1/login", {email:this.email, password:this.password})
                .then((response)=>{
                    localStorage.setItem('Token', response.data.access_token);
                    console.log("Erflogreich");
                    window.location.href = "http://localhost:8080/userinfo"
                });
        },
    }
}
</script>

<style>
.log{
    border: 1px solid lightgray;
    width: 19%;
    margin-left: auto;
    margin-right: auto;
    padding-top: 2rem;
}


.login input{
    display: block;
    margin-right: auto;
    margin-left: auto;
    margin-bottom: 1rem;
    width: 20rem;
    height: 3rem;
    padding-left: 1rem;
}
.login button{
    width: 20rem;
    height: 3rem;
    /* border: 1px solid greenyellow;
    background-color: greenyellow; */
    color: rgb(12, 39, 12);
    cursor: pointer;
    font-size: 1.5em;
    border-radius: 10mm;
}

.login .iconeye{
    position: relative;
    left: 9rem;
    top: 2.3rem;
}

.btns{   
    display: flex;
    flex-direction: column;
    margin: 1rem;
    padding-bottom: 1rem;
    max-width: fit-content;
    margin-left: auto;
    margin-right: auto;
}
#fstbtn{
    margin-bottom: 1rem;
    color: white;
    width: 20rem;
    border-radius: 20mm;
}
#scndbtn{
    margin-bottom: 1rem;
    color: white;
    width: 20rem;
    border-radius: 20mm;
}

</style>