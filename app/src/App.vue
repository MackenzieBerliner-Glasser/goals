<template>
  <div id="app">
    <header>
      <h1>Track Your Goals</h1>
      
      <nav class="nav">
        <router-link to="/">Go <strong>Home</strong></router-link>
        
        <router-link v-if="user" to="/goals">Go to Goals</router-link>
        
        <router-link v-if="user" to="/users">Go to Users</router-link>
        
        <router-link v-if="!user" to="/auth">Sign In</router-link>
        
        <a v-if="user" href="/" @click.prevent="handleSignOut">Sign Out</a>
      </nav>
      <span v-if="user">user: {{ user.email }}</span>
    </header>
    <main>
      <router-view class="content" :onUser="handleUser"></router-view>

      <footer class="footer">
        <p>&copy;MackBG | 2018</p>
      </footer>
    </main>
  </div>
</template>

<script>
import { checkForToken, signOut } from './services/api.js';


export default {
  data() {
    return {
      user: null
    };
  },
  created() {
    this.user = checkForToken();
  },
  methods: {
    handleUser(user) {
      this.user = user;
    },
    handleSignOut() {
      signOut();
      this.user = null;
      this.$router.push('/');
    }
  }
};

</script>

<style>

.nav {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin-left: 5px;
  margin-right: 5px;
}

@media screen and (max-width: 600px) {
    .nav {
    display: flex;
    flex-direction:column;
    width:100%;
    margin: 0;
    }

    a{
      background-color:#E6FDFF;
      color: black;
      border: 1px solid black;
      padding: 3px;
      text-decoration: none;
    }
}

header {
    background-color: black;
    color: white;
    text-align: center;
}

main {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.content {
  flex: 1 0 auto;
}

.footer {
  flex-shrink: 0;
  background-color: black;
  color: white;
}

a {
  background-color:#E6FDFF;
  color: black;
  padding: 3px;
  text-decoration: none;
  margin: 5px;
}
@-webkit-keyframes swing
{
    15%
    {
        -webkit-transform: translateX(5px);
        transform: translateX(5px);
    }
    30%
    {
        -webkit-transform: translateX(-5px);
       transform: translateX(-5px);
    } 
    50%
    {
        -webkit-transform: translateX(3px);
        transform: translateX(3px);
    }
    65%
    {
        -webkit-transform: translateX(-3px);
        transform: translateX(-3px);
    }
    80%
    {
        -webkit-transform: translateX(2px);
        transform: translateX(2px);
    }
    100%
    {
        -webkit-transform: translateX(0);
        transform: translateX(0);
    }
}
@keyframes swing
{
    15%
    {
        -webkit-transform: translateX(5px);
        transform: translateX(5px);
    }
    30%
    {
        -webkit-transform: translateX(-5px);
        transform: translateX(-5px);
    }
    50%
    {
        -webkit-transform: translateX(3px);
        transform: translateX(3px);
    }
    65%
    {
        -webkit-transform: translateX(-3px);
        transform: translateX(-3px);
    }
    80%
    {
        -webkit-transform: translateX(2px);
        transform: translateX(2px);
    }
    100%
    {
        -webkit-transform: translateX(0);
        transform: translateX(0);
    }
}
a:hover {
  background-color: #DBF9F4;
   -webkit-animation: swing 1s ease;
        animation: swing 1s ease;
        -webkit-animation-iteration-count: 1;
        animation-iteration-count: 1;
}

a:active {
  background-color: #383961;
  color: white;
}


span {
  text-align: center;
}
</style>