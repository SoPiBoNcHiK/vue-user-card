<template>
  <div id="app">
    <UserCard v-bind:login="login" :avatar="avatar" :firstname="firstName" :lastname="lastName" :phone="phone" :adress="adress" :email="email"/>
  </div>
</template>

<script>
import UserCard from './components/UserCard.vue'

export default {
  name: 'App',
  components: {
    UserCard
  },
  data(){
    return{
      avatar: '',
      login: '',
      firstName: '',
      lastName: '',
      adress: '',
      phone: '',
      email: '',
    }
  },
  methods: {
    getUserData(){
      this.axios.get('http://37.77.104.246/users/getrandom.php')
        .then( (response)=>{
          this.avatar = response.data.img;
          this.login = response.data.email.split('@')[0];
          this.firstName = response.data.firstName;
          this.lastName = response.data.lastName;
          this.email = response.data.email;
          this.phone = response.data.cellPhone;
        } )
    }
  },
  mounted(){
    this.getUserData();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
