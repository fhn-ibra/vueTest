<template lang="">

  <div class="container">
    <div class="row">
      <div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
        <div class="card border-0 shadow rounded-3 my-5">
          <div class="card-body p-4 p-sm-5">
            <h5 class="card-title text-center mb-5 fw-light fs-5">Sign In</h5>
            <form @submit.prevent='submit'>
              <div class="alert alert-warning" v-if="errors">
                {{ errors }}
            </div>
              <div class="form-floating mb-3">
                <input type="number" v-model="id" class="form-control" id="floatingInput" placeholder="ex. 12121212" required>
                <label for="floatingInput">ID</label>
              </div>
              <div class="form-floating mb-3">
                <input type="password" v-model="password" class="form-control" id="floatingPassword" placeholder="Password" required>
                <label for="floatingPassword">Password</label>
              </div>

              <div class="d-grid">
                <button type="submit" class="btn btn-primary btn-login text-uppercase fw-bold">Sign In</button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios"
import router from "@/router";

export default {

  data() {
    return {
      id: "",
      password: "",
      errors: ""
    }
  },

  mounted() {
    this.token = localStorage.getItem('token');
    if(this.token != null){
      router.push({name: 'home'});
    }
  },

  methods: {
    submit() {
      axios.post('http://localhost:8000/api/login', {
        id_card_number: this.id,
        password: this.password
      })
        .then(function (response) {
          localStorage.setItem("id", response.data.id);
          localStorage.setItem("id_card_number", response.data.id_card_number);
          localStorage.setItem("name", response.data.name);
          localStorage.setItem("born_date", response.data.born_date);
          localStorage.setItem("gender", response.data.gender);
          localStorage.setItem("address", response.data.address);
          localStorage.setItem("regional_id", response.data.regional_id);
          localStorage.setItem("token", response.data.login_tokens);
          localStorage.setItem("regional", JSON.stringify(response.data.regional));

          router.push('/');
        })
        .catch((error)  => {
          this.errors = error.response.data.message;
        });
    }


  },
}
</script>
<style lang="">

</style>