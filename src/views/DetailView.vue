<template>
  <div class="detail">
    <h1>User detail</h1>
    <h3 class="msg"> {{msg}} </h3>

     <!-- <form> -->
        <label for="fname">User Name</label>
        <input type="text" id="fname" name="userName" v-model="user.name">

        <label for="email">Email</label>
        <input type="text" id="email" name="email" v-model="user.email">

        <label for="phone">Phone</label>
        <input type="text" id="phone" name="phone" v-model="user.phone">

        <label for="country">Role</label>
        <select v-model="selected">
            <option v-for="item in roleOptions" :value="item" :key="item">{{item}}</option>
        </select>
        <input type="submit" value="Submit" v-on:click="handleEditUser">
      <!-- </form> -->
  </div>

</template>

<script>

export default {
  name: "detail",
  // props: ['user'],
  data() {
    return {
      user: {},
      listUser: [],
      roleOptions: ['System Admin', 'Chatter Free User', 'IT Manager'],
      selected: '',
      msg: ''
    }
  },
  methods: {
    getAllUserData() {
      var userData = localStorage.getItem("user");
      if(userData) {
        return this.listUser = JSON.parse(userData);
      }
    },

    handleEditUser() {
      var users = this.listUser.map(u => u.id !== this.user.id ? u : this.user);
      localStorage.removeItem('user');
      localStorage.setItem('user', JSON.stringify(users));
      this.$emit('renderDataUser');
      this.msg = 'Update data successed!';
    }
  },
  mounted() {
    let userId = this.$route.params.id;
    if (userId) {
      var userData = localStorage.getItem("user");
      this.listUser = JSON.parse(userData);
      const users =  this.listUser.filter(element => {
          return element.id === userId;
        });
        this.user = users[0];
        this.selected = this.user.role;
    }
  }
};
</script>

<style scoped>
.msg {
  color: rgb(40, 132, 73);
  text-align: center;
}
 .detail  {
    width: 40rem;
    margin: 0 auto;
    /* padding-top: 10rem; */
    padding: 10rem 0.5rem 0.5rem 0.5rem;
}

h1 {
  text-align: center;
}

/* Style inputs */
  input[type=text], select {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

/* Style the submit button */
input[type=submit] {
  width: 100%;
  background-color: #04AA6D;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

/* Add a background color to the submit button on mouse-over */
input[type=submit]:hover {
  background-color: #45a049;
}
</style>

