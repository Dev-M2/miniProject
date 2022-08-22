<template>
  <!-- <div class="nav">
  </div> -->

  <div id="home">
      <div>
        <div> </div>
        <form class="form-group"> 
          <div class="item"> 
              <label>Name</label>
              <input type="text" v-model="userName" placeholder="User name" />
          </div>
          <div class="item">
            <label>Role</label>
            <select v-model="selected">
                <option v-for="item in roleOptions" :value="item" :key="item">{{item}}</option>
            </select>
          </div>
          <div class="item">
            <button type="button" class="btn-search" @click="doSearch()">Search</button>
            <button type="button" class="btn-addnew" @click="showModal()">Add New</button>
          </div>
        </form>
        <!-- Modal Add new User -->
        <modalAddNew v-bind:pRoles="roleOptions" v-show="isModalVisible" @close="closeModal" @createUser="doAddNew"/>
        <div id="logout">
          <router-link to="/">Logout</router-link>
        </div>
    </div>

    <div>
        <table id="customers">
            <thead>
            <tr>
                <th>No.</th>
                <th>Id</th>
                <th>Name</th>
                <th>Email</th>
                <th>Phone</th>
                <th>Role</th>
                <th>Action</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(user, index) in users" :key="user.id">
                <td>{{index + 1}}</td>
                <td>{{user.id}}</td>
                <td>{{user.name}}</td>
                <td>{{user.email}}</td>
                <td>{{user.phone}}</td>
                <td>{{user.role}}</td>
                <td>
                  <button type="button" class="btn-edit" @click="doEditUser(user)">Detail</button>
                  <button type="button" class="btn-delete" @click.stop.prevent="doDeleteUser(index)">Delete</button>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
  </div>
</template>

<script>
import modalAddNew from './AddNewView.vue';
    export default {
        name: "Home",
        components: {
          modalAddNew,
        },
        data() {
            return {
                users: [],
                listUser: [],
                selected: '',
                roleOptions: ['','System Admin', 'Chatter Free User', 'IT Manager'],
                userName: "",
                emailReg: "",
                passwordReg: "",
                confirmReg: "",
                isModalVisible: false,
                // isDetailVisible: true
            }
            
        },
        methods: {
            doSearch() {
              this.getAllUser();
              var results = [];
              if(this.userName) {
                results = this.listUser.filter(element => {
                  return element.name.includes(this.userName);
                });
              } else {
                results = this.listUser;
              }

              if (this.selected && this.selected != '') {
                results = results.filter(el => {
                  return el.role === this.selected;
                });
              }

              this.users = results;
            },

            doAddNew(value) {
              this.users.push(value);
              this.fetchDataUser(this.users)
            },

            doEditUser(user) {
              const routeData  = this.$router.resolve({name: 'detail', params: { id: user.id }});
              window.open(routeData.href, "_blank");

            },

            doDeleteUser(index) {
              this.users.splice(index, 1);
              this.fetchDataUser(this.users)
            },
            showModal() {
              this.isModalVisible = true;
            },
            closeModal() {
              this.isModalVisible = false;
            },
            getAllUser() {
              var userData = localStorage.getItem("user");
              if(userData) {
                return this.listUser = JSON.parse(userData);
              }
          },
          fetchDataUser(valUser) {
            if(valUser) {
              localStorage.removeItem('user');
              localStorage.setItem('user', JSON.stringify(valUser));
            }
          }

        },
        mounted() {
          this.getAllUser();
          this.users = this.listUser;
        }
    }
</script>

<style scoped>

  #home {
    padding: 10rem 2rem 2rem 2rem;
  }

  #logout {
    float: right;
    padding-top: 2.5rem;
  }

  #add-new {
    margin-bottom: 1rem;
  }

  .detail-view {
    display: none;
  }
  .user-reg {
    padding: 0.5rem;
  }
   .btn-add-new {
      background-color: #04AA6D;
      color: white;
      padding: 8px 10px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
   }
  .form-group {
    display: inline-flex;
  }
  .item {
    display: inline-flex;
    margin: 1rem 1rem;
  }

  /* Button in td */
  .btn-search {
      background-color: #04aa6d; /* Green */
      border: none;
      color: white;
      padding: 8px 15px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 16px;
      margin: 0rem 0.5rem 0.25rem 0.25rem;
      border-radius: 0.25rem;
      cursor: pointer;
  }
  .btn-addnew {
      background-color: #008CBA; /* Green */
      border: none;
      color: white;
      padding: 8px 15px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 16px;
      margin: 0rem 0.5rem 0.25rem 0.25rem;
      border-radius: 0.25rem;
      cursor: pointer;
  }
  .btn-edit {
      background-color: #4CAF50; /* Green */
      border: none;
      color: white;
      padding: 8px 18px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 16px;
      margin: 0.25rem 0.5rem 0.25rem 0.25rem;
      border-radius: 0.25rem;
      cursor: pointer;
  }
  .btn-delete {
      background-color: #f44336; /* Red */
      border: none;
      color: white;
      padding: 8px 18px;
      text-align: center;
      text-decoration: none;
      display: inline-block;
      font-size: 16px;
      margin: 0.25rem 0.5rem 0.25rem 0.25rem;
      border-radius: 0.25rem;
      cursor: pointer;
  }

  /* Style inputs, select elements and textareas */
   input[type=text], select, textarea{
      width: 100%;
      padding: 12px;
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
      /* float: right; */
   }

  #customers {
    font-family: Arial, Helvetica, sans-serif;
    border-collapse: collapse;
    width: 100%;
  }

  #customers td, #customers th {
    border: 1px solid #ddd;
    padding: 8px;
  }

  #customers tr:nth-child(even){background-color: #f2f2f2;}

  #customers tr:hover {background-color: #ddd;}

  #customers th {
    padding-top: 12px;
    padding-bottom: 12px;
    text-align: left;
    background-color: #04AA6D;
    color: white;
    font-weight: 800;
  }

</style>