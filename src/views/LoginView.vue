
<template>
 <div class="login-page">
      <transition name="fade">
         <div v-if="!registerActive" class="wallpaper-login"></div>
      </transition>
      <div class="wallpaper-register"></div>

      <div class="container">
         <div class="row">
            <div class="col-lg-4 col-md-6 col-sm-8 mx-auto">
               <div v-if="!registerActive" class="card login" v-bind:class="{ error: emptyFields }">
                  <h1>Sign In</h1>
                     <p class="msg"> {{msgError}} </p>
                  <!-- <form class="form-group"> -->
                  <div class="form-group">
                     <div class="row">
                        <input v-model="username" type="text" class="form-control" placeholder="User Name" required>
                     </div>
                     <div class="row">
                        <input v-model="password" type="password" class="form-control" placeholder="Password" required>
                     </div>
                     <div class="row">
                        <input type="submit" class="btn btn-primary" @click="doLogin">
                     </div>
                     <p>Don't have an account? <a href="#" @click="registerActive = !registerActive, emptyFields = false">Sign up here</a>
                     </p>
                     <!-- <p><a href="#">Forgot your password?</a></p> -->
                  <!-- </form> -->
                  </div>
               </div>

               <div v-else class="card register" v-bind:class="{ error: emptyFields }">
                  <h1>Sign Up</h1>
                  <form class="form-group">
                     <div class="row">
                        <input v-model="emailReg" type="email" class="form-control" placeholder="Email" required>
                     </div>
                     <div class="row">
                        <input v-model="passwordReg" type="password" class="form-control" placeholder="Password" required>
                     </div>
                     <div class="row">
                        <input v-model="confirmReg" type="password" class="form-control" placeholder="Confirm Password" required>
                     </div>
                     <div class="row">
                        <input type="submit" class="btn btn-primary" @click="doRegister">
                     </div>
                     <p>Already have an account? <a href="#" @click="registerActive = !registerActive, emptyFields = false">Sign in here</a>
                     </p>
                  </form>
               </div>
            </div>
         </div>

      </div>
   </div>
</template>

<script>

export default {
  name: "Login",
  data() {
    return {
        registerActive: false,
        username: "",
        password: "",
        emailReg: "",
        passwordReg: "",
        confirmReg: "",
        emptyFields: false,
        listUser: [],
        msgError: ''
    }
  },
  methods: {
      doLogin() {
         this.getAllUser();

         if (this.username === "" || this.password === "") {
            this.emptyFields = true;
         } else {
            const results = this.listUser.filter(element => {
               return element.name === this.username && element.password === this.password;
            });

            if(results != '') {
               this.$router.push('/home');
            } else {
               this.msgError = 'Login fail!';
            }
         }
      },
      
      doRegister() {
         if (this.emailReg === "" || this.passwordReg === "" || this.confirmReg === "") {
            this.emptyFields = true;
         } else {
            this.$router.push('/home');
         }
      },
      getAllUser() {
         var userData = localStorage.getItem("user");
         if(userData) {
            return this.listUser = JSON.parse(userData);
         }
      }
   }
};
</script>

<style scoped>

p {
   line-height: 1rem;
}

.msg {
   color: red;
}
.card {
   padding: 20px;
}

.form-group input {
    margin-bottom: 15px;
}
.form-control {
    display: block;
    width: 88%;
    height: calc(1.5rem + 1px);
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    line-height: 1.5;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color .15s ease-in-out,box-shadow .15s ease-in-out;
}

.login-page {
   align-items: center;
   display: flex;
   height: 100vh;
   justify-content: center;
}
   /* Style inputs, select elements and textareas */
   input[type=text], select, textarea{
    width: 95%;
    padding: 19px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    resize: vertical;
   }

   /* Style the label to display next to the inputs */
   label {
    padding: 12px 12px 12px 0;
    display: inline-block;
   }

   /* Style the submit button */
   input[type=submit] {
    background-color: #04AA6D;
    color: white;
    padding: 12px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    text-align: center;
   }

   /* Style the container */
   .container {
    border-radius: 5px;
    background-color: #d7d3d3;
    width: 24rem;
    /* padding: 20px; */
   }

   /* Floating column for labels: 25% width */
   .col-25 {
    float: left;
    width: 25%;
    margin-top: 6px;
   }

   /* Floating column for inputs: 75% width */
   .col-75 {    
    float: left;
    width: 75%;
    margin-top: 6px;
   }

   /* Clear floats after the columns */
   .row:after {
    content: "";
    display: table;
    clear: both;
   }

   /* Responsive layout - when the screen is less than 600px wide, make the two columns stack on top of each other instead of next to each other */
      @media screen and (max-width: 600px) {
      .col-25, .col-75, input[type=submit] {
         width: 100%;
         margin-top: 0;
      }
   }
</style>