<template>
  <div class="body">
    <div class="login-container">
      <h2>Login</h2>
      <form id="loginForm">
        <label for="username">Kullanıcı Adı:</label>
        <input type="text" id="username" name="username" >

        <label for="password">Şifre:</label>
        <input type="password" id="password" name="password" >

        <button type="button" @click="login">Giriş Yap</button>

        <div v-if="ctrl" class="uyari">
          <p v-if="ok">BASARİLİ GİRİŞ</p>
          <p v-else>basarisiz</p>
        </div>
        
      </form>
    </div>
  </div>
</template>

<script>
import players from "../mydts/mydata"
import MainPage from '../components/MainPage.vue'
export default {
  name: 'HomeView',
  components:{
    MainPage
  },
  data: function () {
    return {
      veri: players,
      ctrl: false,
      ok:true,
      username : "",
      pass : ""
    }
  },
  methods: {
    qualif(){
      var username = document.getElementById('username').value;
      var password = document.getElementById('password').value;
      var quaf= false
      for (let index = 0; index < players.length; index++) {
        if(players[index].username===username && players[index].pass===password){
             this.username=username
             this.pass=password
             quaf=true
           }}
      return quaf;
     },
    login() {
      
      if (this.qualif()) {
        this.ok = true;
        this.ctrl = true;
        setTimeout(() => {
          this.$router.push("/MainPage")
        }, 3000);
        

      } else {
        this.ctrl = true;
        this.ok = false;
      }
    }
  },
  beforeRouteLeave(to,from,next){
    if (confirm("eminmisiniz")){
    next();}
    else{
      
      this.ctrl=false
    }
  }
}
</script>

<style scoped>
.body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
}

.login-container {
  background-color: #4e2ddf;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(63, 36, 218, 0.1);
}

label {
  display: block;
  margin-bottom: 8px;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 16px;
  box-sizing: border-box;
}

button {
  background-color: #4caf50;
  color: #fff;
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  width: 100%;
}

.uyari {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: red;
  margin-top: 20px;
  padding: 15px;
}
</style>
