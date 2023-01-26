<template>
  <div v-if="loggy == 0" class="home">
    <h1 id="besttitle">Login Form</h1>
    <div>
      <div class="imgcontainer">
        <img src="../assets/Avatar.png" alt="Avatar" class="avatarx" />
      </div>
      <p>Please fill all fields to register an account</p>


      <div class="container">
        <hr />
        <label for="uname"><b class="lefty">Email</b></label>
        <input
          type="email" placeholder="Email de utilizador" name="uname" required v-model="email_"/>

        <label for="psw"><b class="lefty">Password</b></label>
        <input type="password" placeholder="Introduza a sua password" name="psw" required v-model="pass_" v-on:keyup.enter="signupRequest()"/>

        <hr />
        <button type="submit" class="buttonnn" @click="signupRequest()">Login</button>
        
      </div>
      <div class="container_signin">
          <p>Don't have an account? <router-link to="/about">Register</router-link></p>
        </div>
    </div>
    <div v-if="alert == 1">
      <div class="alert alert-success" role="alert">
        Login feito com sucesso
      </div>
    </div>
  </div>

  <div v-if="loggy==1">
    <div class="notlogged">You are already logged in</div>
    <img src="../assets/403.jpg" alt="nope" class="nope" />
  </div>

</template>

<script>
export default {
  data() {
    return {
      loggy: 0,
      alert: 0,
      email_: "",
      pass_: "",
      email: "",
      pass:"",
    }},

  mounted(){ 
    this.addy = localStorage.getItem('admin')
    this.loggy = localStorage.getItem('logged')
    this.email = localStorage.getItem('email')
    this.pass = localStorage.getItem('pass')
  },

  methods: {
    signupRequest() {
      
      this.successMessage = "login Successfull."
      this.alerta = 1
      if (this.email_ == "admin_email@gmail.com"){                                 
                localStorage.setItem('admin', 1)                                  
          this.$router.push("/adminView");
          location.reload(); 
        }                                                                                
      else if (this.email_ == this.email && this.pass_ == this.pass) {
        localStorage.setItem('logged', 1)
        location.reload();
        }                                           
      error => {
        let errorResponse = JSON.parse(error.message);
        this.errorMessage = errorResponse.error.message;
      }
    },
  }
}

</script>

<style>
.notlogged{
  font-weight: bold;
  font-size: 35px;
}

.nope {
  width:50%;
  margin-top: 15px;
}

.container_signin {
  background-color: #f1f1f1;
  text-align: center;
  padding: 16px;
  width: 33%;
  display: block;
  margin-left: auto;
  margin-right: auto;
  border-radius: 25px;
}

hr {
  border: 1px solid #f1f1f1;
  margin-bottom: 25px;
}


#besttitle {
  text-decoration: underline;
  
  font-weight: bold;
  margin-top: 30px;
  margin-bottom: 30px;
  color: green;
}

.lefty {
  display: flex;
  align-self: left;
  color: green;
  margin-left: 20px;
}

form {
  border: 3px solid #f1f1f1;
}

input[type="email"],
input[type="password"] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
  background-color: #f1f1f1;
}

input[type="email"]:focus,
input[type="password"]:focus {
  background-color: #ddd;
  outline: none;
}

.buttonnn {
  background-color: #04aa6d;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 100%;
  border-radius: 50px;
}

.buttonnn:hover {
  opacity: 0.5;
}

.cancelbtn {
  width: auto;
  padding: 10px 18px;
  background-color: #f44336;
}

.imgcontainer {
  text-align: center;
  margin: 24px 0 12px 0;
}

img.avatar {
  width: 40%;
  border-radius: 50%;
}

.container {
  padding: 16px;
  width: 35%;
  display: block;
  margin-left: auto;
  margin-right: auto;
  border-radius: 25px;
}

.container_rem {
  margin-top: 10px;
  padding: 12px;
  border-radius: 25px;
  width: 35%;
  margin-left: auto;
  margin-right: auto;
}

.avatar {
  width: 60px;
}

span.psw {
  float: right;
  padding-top: 16px;
}

@media screen and (max-width: 300px) {
  span.psw {
    display: block;
    float: none;
  }
  .cancelbtn {
    width: 100%;
  }
}
</style>