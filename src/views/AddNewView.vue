<script>
  export default {
    name: 'addnew',
    props: ['pRoles'],
    data() {
      return {
         roleOptions: this.pRoles,
         selected: 'System Admin',
         userName: '',
         phone: '',
         password: ''
      }
    },
    methods: {
      close() {
        this.$emit('close');
      },
      emitParentcreateUser() {
         const newUser = {id: '0052v00000bX0m1AAC', name : this.userName , email: 'AutomatedProcess@yopmail.com', phone: this.phone, role: this.selected, password: this.password};
         this.$emit('createUser', newUser);
         this.resetInput();
         this.close();
      },
      resetInput() {
        this.userName = '';
        this.phone = '';
        this.password = '';
      }

    },
  };
</script>

<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal" role="dialog" aria-labelledby="modalTitle" aria-describedby="modalDescription">
        <header class="modal-header" id="modalTitle">
          <slot name="header">Create a new User</slot>
          <button
            type="button"
            class="btn-close"
            @click="close"
            aria-label="Close modal">
            x
          </button>
        </header>

        <section class="modal-body" id="modalDescription">
          <div class="body">
            <div class="item"> 
              <label>Name</label>
              <input type="text" v-model="userName" placeholder="User name" required />
            </div>
            <div class="item">
               <label>Role</label>
               <select v-model="selected">
                  <option v-for="item in roleOptions" :value="item" :key="item">{{item}}</option>
               </select>
            </div>
            <div class="item"> 
               <label>Phone</label>
               <input v-model="phone" type="text" placeholder="Phone" />
            </div>
            <div class="item"> 
               <label>Password</label>
               <input v-model="password" type="password" placeholder="Password" required />
            </div>
          </div>
        </section>

        <footer class="modal-footer">
          <button type="button" class="btn-green" @click="emitParentcreateUser" aria-label="Create User">Submit</button>
        </footer>
      </div>
    </div>
  </transition>
</template>

<style scoped>
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
    width: 40rem;
    height: 33rem;
    border-radius: 0.25rem;
    padding: 1rem 1rem 1rem 1rem;
  }

  .modal-header,
  .modal-footer {
    padding: 15px;
    display: flex;
  }

  .modal-header {
    position: relative;
    border-bottom: 1px solid #eeeeee;
    color: #18b67c;
    justify-content: center;
    font-weight: 800;
    font-size: 20px;
  }

  .modal-footer {
    border-top: 1px solid #eeeeee;
    flex-direction: column;
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    position: absolute;
    top: 0;
    right: 0;
    border: none;
    font-size: 20px;
    padding: 10px;
    cursor: pointer;
    font-weight: bold;
    color: #04AA6D;
    background: transparent;
  }

  .btn-green {
    color: white;
    background: #03774c;
    border: 1px solid #03774c;
    border-radius: 2px;
    padding: 0.5rem;
    font-size: 18px;
  }

  .modal-fade-enter,
  .modal-fade-leave-to {
    opacity: 0;
  }

  .modal-fade-enter-active,
  .modal-fade-leave-active {
    transition: opacity .5s ease;
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

   input[type=password], select, textarea{
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
</style>