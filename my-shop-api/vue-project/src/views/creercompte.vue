<template>
    <div>
      <form>
        <h3>Créer un compte</h3>

        <label class="label" for="email">Email</label>
        <input id= "email" type="text" placeholder="email" required/>
        <label class="label" for="fullname">fullname</label>
        <input id= "fullname" class="input" type="text" placeholder="fullname" required/>
        <label class="label" for="password">Password</label>
        <input id = "password" type="password" placeholder="password" required/>
        <button type="button" class="submit" @click="registerUser">Créer compte</button>
        <div class="seconnecter">
          <router-link to="/login">Se connecter</router-link>
        </div>
      </form>
    </div>
  </template>

<script>
import axios from 'axios';
export default {
  methods: {
    registerUser() {
      const email = document.getElementById('email').value;
      const password = document.getElementById('password').value;
      const fullname = document.getElementById('fullname').value;
      const token = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyNDU1MDAsImV4cCI6MTcwMDI0OTEwMCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImFudG9pbmUubG9wZXpAZXBpdGVjaC5kaWdpdGFsIn0.A2gkcfA7gxj-CXmxq9SjDGyfoXlZEjlzLBEscOpOdip6O4wkXdhRoKRzDKy5_wlWk-f7OYDQJDhfw14FZz-e1edXbHAKM3mM4kjpbkMNZITus5Det3qPiraRj0gGKjFyVVThaXTwjOBUmWFp6da027UrrNp7CORJmu1RqA8ffyDvq9cMHey1uW7LNWDvG2zI5H9TelnTXXzn8lBaN6IKDLQfCouE-uhbGPmbl1kXoVW8nxjLY7knMI67KCpkpIA0qsPsZ93OBVNA35dwlgPlxqJEVt5BjdFx2iTvH9bCGAhf0-KSkv5EC6UII0KQsku6BfeO73G0DivCIwpyvzGnzQ';
      axios.post('http://localhost/api/users', {
        email: email,
        password: password,
        fullName: fullname
      },
      {
         headers: {
           'Authorization': `Bearer ${token}`
         },
         timeout: 5000 // temps d'attente en millisecondes
       })
       .then(response => {
        console.log(response.data);

       })
       .catch(error => {
    console.error( error);
});
      this.open_admin();
    },
     open_admin() {
      const url_window = 'http://localhost:5173/admin';
      window.open(url_window, '_blank');
    },
   }
}

</script>

<style>
* {
    margin: 0;
    box-sizing: border-box;
}
body{
    background-color: #ffffff;
}

form{
    height: 600px;
    width: 400px;
    background-color: rgba(255, 255, 255, 0.13);
    position: absolute;
    transform: translate(-50%,-50%);
    top: 50%;
    left: 50%;
    border-radius: 10px;
    backdrop-filter: blur(10px);
    border: 2px solid rgba(255,255,255,0.1);
    box-shadow: 0 0 40px rgba(8,7,16,0.6);
    padding: 50px 35px;
}
form *{
    font-family: 'Poppins',sans-serif;
    color: #ffffff;
    letter-spacing: 0.5px;
    outline: none;
    border: none;
}
form h3{
    font-size: 32px;
    font-weight: 500;
    line-height: 42px;
    text-align: center;
    color: #000000;

}

.label{
    display: block;
    margin-top: 30px;
    font-size: 16px;
    font-weight: 500;
    color: #080710;
}
input#fullname, input#password, input#email {
    display: block;
    height: 50px;
    width: 100%;
    background-color: rgba(255,255,255,0.07);
    border-radius: 8px;
    padding: 0 10px;
    margin-top: 8px;
    font-size: 14px;
    font-weight: 300;
    color: #080710;
    border: 2px solid rgba(0, 0, 0, 0.1);

}
::placeholder{
    color: #535353;
}
.submit {
    margin-top: 50px;
    width: 100%;
    background-color: #434343;
    color: #ffffff;
    padding: 15px 0;
    font-size: 18px;
    font-weight: 600;
    border-radius: 5px;
    cursor: pointer;
}
.seconnecter{
  margin-top: 30px;
  display: flex;
  padding-left: 110px;

}

a{
    text-decoration:none;
}

.seconnecter a {
    color: #000000;
}

</style>