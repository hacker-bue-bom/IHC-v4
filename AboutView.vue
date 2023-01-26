<template>
  <div v-if="loggy == 0" class="regi">
    <div class="container">
      <h1 class="b">Registration Form</h1>
      <p>Please fill all fields to register an account</p>
      <hr />
    
      <label for="email"><b class="lefty">Email</b></label>
      <input
        type="email"
        placeholder="insert a valid email"
        name="email"
        id="email_id"
        v-model="email_temp"
      />

      <label for="psw"><b class="lefty">Password</b></label>
      <input
        type="password"
        placeholder="Insert your Password"
        name="psw"
        id="psw"
        v-model="psw_temp"
      />

      <label for="psw-repeat"><b class="lefty">Confirmar Password</b></label>
      <input
        type="password"
        placeholder="Repeat the Password"
        name="psw-repeat"
        id="psw-repeat"
        v-model="psw_temp2"
      />
      <hr />
      <button @click="addnewuser()" type="submit" class="registerbtn">
        Register
      </button>
    </div>

    <div v-if="alerta > 0" class="popup-overlay">
      <div class="popup-content">
        <!-- Popup content here -->
    <div v-if="alerta == 1">
      <div class="alert alert-success" role="alert">
        Success! Your account has been created!
        <br>
        <router-link  :to="'/Login'" @click="alerta = 0">
          <button class="suc">Login</button>
        </router-link>
      </div>
    </div>

    <div v-if="alerta == 2">
      <div class="alert alert-danger" role="alert">
        You need a valid Email to register an account
      </div>
      <button class="redbtn" @click="alerta = 0">Close</button>
    </div>

    <div v-if="alerta == 3">
      <div class="alert alert-danger" role="alert">
        You need to introduce a Password and confirm it
      </div>
      <button class="redbtn" @click="alerta = 0">Close</button>
    </div>

    <div v-if="alerta == 4">
      <div class="alert alert-danger" role="alert">
        Your passwords don't match
      </div>
      <button class="redbtn" @click="alerta = 0">Close</button>
    </div>

    <div v-if="alerta == 5">
      <div class="alert alert-danger" role="alert">
        Please introduce a valid email
      </div>
      <button class="redbtn" @click="alerta = 0">Close</button>
    </div>


      </div>
    </div>

    <div class="container_signin">
      <p>Already have an account? <router-link to="/Login">Login</router-link></p>
    </div>
    
  </div>

  <div v-if="loggy==1">
    <div class="notlogged">You can't access this area if you already have an account</div>
    <img src="../assets/403.jpg" alt="nope" class="nope" />
  </div>
</template>



<script>

export default {
  el: "#app",
  data() {
    return {
      loggy: 3,
      addy:0,
      alerta: "",
      email_temp: "", //guarda temporatiamente um email (certifica-te que o method "apaga" estes dados depois de serem introduzidos no "users")
      psw_temp: "", //guarda temporatiamente uma password (certifica-te que o method "apaga" estes dados depois de serem introduzidos no "users")
      psw_temp2: "", //guarda temporatiamente outra password para comprarmos com o 1º (certifica-te que o method "apaga" estes dados depois da comparacao)
    };
  },

  mounted(){ 
    this.addy = localStorage.getItem('admin')
    this.loggy = localStorage.getItem('logged')
    
  },

  methods: {
    isValidEmail() {
      let count = 0;
      for(let i = 0; i < this.email_temp.length; i++) {
        if (this.email_temp[i] === "@") {
        count++;
      }
      }

      let Index = this.email_temp.indexOf("@");
      let check = this.email_temp.indexOf(".", Index) !== -1;

   return count === 1 && check;
    },

    addnewuser: function () {


      if (this.psw_temp != "" && this.psw_temp == this.psw_temp2 && this.isValidEmail()==true) {
        //primeiro verificamos se ambas as passwords introduzidas sao iguais
        this.x +=1
        localStorage.setItem('email', this.email_temp)
        localStorage.setItem('pass', this.psw_temp)
        localStorage.setItem('logged', 1)
        this.alerta = 1;

      } //aqui ficam os alerts no caso de dar erro
      else if (this.isValidEmail()==false) {
        this.alerta = 5;
      }
      else if (this.email_temp == "") {
        this.alerta = 2;
      } else if (this.psw_temp == "" || this.psw_temp2 == "") {
        this.alerta = 3;
      } else if (this.psw_temp != this.psw_temp2) {
        this.alerta = 4;
      }
    },



  },
};

//export var users2 = users
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


.alert-danger{width: 2000px;}
  
.redbtn{
  background-color: rgb(170, 13, 13);
  color: white;
  padding: 16px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  border-radius: 50px;
  height: auto;    
  font-weight: bold;
}
.redbtn:hover{
  opacity: 0.5;
}

.suc{
  background-color: #04aa6d;
  color: white;
  padding: 16px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 20%;
  border-radius: 50px;
  height: auto;    
  font-weight: bold;
}
.suc:hover {
  opacity: 0.5;
}

.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1;
}

.popup-content {
  position:absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: pink;
  padding: 20px;
  border: 5px solid rgb(116, 3, 3);
  border-radius: 20px;
  padding: 5px;

  color: rgb(170, 14, 14);
    font-weight: bold;
    font-size: 1.5em;
}

.alert-success{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: rgb(158, 228, 158);
  padding: 20px;
  border: 5px solid darkgreen;
  border-radius: 20px;
  padding: 5px;
  color: green;
  font-weight: bold;
  font-size: 1em;
  width: 700px;
}

.b {
  color: green;
  font-weight: bold;
  text-decoration: underline;
  
}

.lefty {
  display: flex;
  align-self: left;
  color: green;
  margin-left: 20px;
}

* {
  box-sizing: border-box;
}

.container {
  padding: 16px;
  width: 35%;
  display: block;
  margin-left: auto;
  margin-right: auto;
  border-radius: 25px;
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

hr {
  border: 1px solid #f1f1f1;
  margin-bottom: 25px;
}

.registerbtn {
  background-color: #04aa6d;
  color: white;
  padding: 16px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 100%;
  border-radius: 50px;
}

.registerbtn:hover {
  opacity: 0.5;
}

a {
  color: dodgerblue;
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
</style>