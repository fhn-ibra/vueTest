<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header v-if="$route.name != 'Login'">
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
          aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <RouterLink to="/" class="nav-link active">Home</RouterLink>
            </li>
            <li class="nav-item">
              <button @click="logout()" class="nav-link">Logout</button>
            </li>
          </ul>
          <span class="navbar-text">
           Halo, {{ nama }}
          </span>
        </div>
      </div>
    </nav>
  </header>


  <RouterView />
</template>

<script>
import axios from 'axios'
import router from './router';

export default {
  data(){
    return{
      nama: localStorage.getItem('name'),
    }
  },

  methods: {
    logout() {
      axios.post('http://localhost:8000/api/logout',null, {
        headers: {
          "Authorization": `Bearer ${localStorage.getItem('token')}`
        }
      })
        .then(function (response) {
          localStorage.removeItem("id")
          localStorage.removeItem("id_card_number")
          localStorage.removeItem("name")
          localStorage.removeItem("born_date")
          localStorage.removeItem("gender")
          localStorage.removeItem("address")
          localStorage.removeItem("regional_id")
          localStorage.removeItem("token")
          localStorage.removeItem("regional")

          router.push('Login');
        })
        .catch(function (error) {
          console.log(error);
        });
    }
  },
}
</script>
