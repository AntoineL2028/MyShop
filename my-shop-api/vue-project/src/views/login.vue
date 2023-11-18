<template>
  <div>
    <form id="login-form">
      <h3>Login</h3>

      <label for="email">email</label>
      <input id="email" type="text" placeholder="email" />

      <label for="password">password</label>
      <input id="password" type="password" placeholder="password" />

      <button class="submit" v-on:click="loginUser"> login </button>
      <div class="creercompte">
        <router-link to="/creercompte">Créer un compte</router-link>
      </div>
      <div id="erreur"><p id="erreurlogin" class="erreurlogin"> </p></div>

    </form>
  </div>
</template>
  
<style>
.creercompte a {
  color: rgb(0, 0, 0);
}

.creercompte {
  padding-left: 99px;
  padding-top: 40px;
}

input#passwords,
input#emails {
  display: block;
  height: 50px;
  width: 100%;
  background-color: rgba(255, 255, 255, 0.07);
  border-radius: 8px;
  padding: 0 10px;
  margin-top: 8px;
  font-size: 14px;
  font-weight: 300;
  color: #080710;
  border: 2px solid rgba(0, 0, 0, 0.1);
}
</style>

<script>
import axios from 'axios';
import router from '../router';
export default {
  methods: {
    loginUser() {
      const loginForm = document.getElementById('login-form');
      loginForm.addEventListener('submit', event => {
        event.preventDefault();
        const email = document.getElementById('email').value;
        const password = document.getElementById('password').value;
        axios.post('http://localhost/authentication_token', {
          email: email,
          password: password,
        })
          .then(response => {

            const status = response.status;
            console.log(status)
            if (status == 200) { // Si le status est 200 alors ça veut dire que les informations rentré par l'utilisateur sont correctes
              router.push('/admin');
            }
          }
          )
          .catch(error => {
                if (error.response.status === 401) {
                    document.querySelector("#erreurlogin").innerHTML = "the password or the email is invalid";
                } else {
                    console.log(error);
                }
              });
      });
    },
   
  }
}
</script>