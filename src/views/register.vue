<template>
    <div >
        <div class="register">
            <input v-model="email" type="text" placeholder="Email eingeben">
            <input v-model="name" type="text" placeholder="Name eingeben">
            <input v-model="phone" type="text" placeholder="Telefon eingeben">
            <span class="iconeye fa-regular fa-eye" v-on:click="ShowHidePW" style="cursor: pointer">
            
            </span>
            <input v-model="password" id="pw" type="password" placeholder="Passwort eingeben"> 
            <input v-model="passwordComf" id="pw" type="password" placeholder="Passwort erneut eingeben"> 
            <div class="termsstyle">
            <p>Terms:</p><input v-model="terms" type="checkbox" name="Terms" id="terms">
            </div>
            <button class="btn btn-success" @click="sendData">Register</button>
        </div>
    </div>
</template>




<script>
import $ from'jquery'
import axios from 'axios'


export default {
    name:'register',
    data(){
        return {
            email:"",
            name:"",
            phone:"",
            password:"",
            passwordComf:"",
            terms:false,

        }
    },
    methods:{
        ShowHidePW(){  
                $(this).toggleClass("fa-eye fa-eye-slash");

                if ($('#pw').attr("type") == "password") {
                    $('#pw').attr("type", "text");
                } else {
                    $('#pw').attr("type", "password");
                }         
        },
        sendData(){
            if(this.password == this.passwordComf){
            axios.post("https://api.essimo.io/api/v1/register", {email:this.email, password:this.password, name:this.name, phone:this.phone, passwordConfirmation:this.passwordComf, terms:this.terms})
                .then((response)=>{
                    localStorage.setItem('Token', response.data.access_token);
                    console.log("Erflogreich");
                    window.location.href = "http://localhost:8080/userinfo"

                });
        }else{alert("Passwörter stimmen nicht überein")}
        },
    }
}
</script>

<style>
.register input{
    display: block;
    margin-right: auto;
    margin-left: auto;
    margin-bottom: 1rem;
    width: 20rem;
    height: 3rem;
    padding-left: 1rem;
}
.register button{
    width: 20rem;
    /* height: 3rem; */
    /* border: 1px solid greenyellow;
    background-color: greenyellow; */
    color: rgb(12, 39, 12);
    cursor: pointer;
    font-size: 1.5em;
    border-radius: 10mm;
}

.register .iconeye{
    position: relative;
    left: 9rem;
    top: 2.3rem;
}
.termsstyle input{
    width: 1rem;
}
.termsstyle{
display: flex;
max-width: fit-content;
margin-left: auto;
margin-right: auto;
}
#terms{
    margin-top: -0.67rem;
}

</style>