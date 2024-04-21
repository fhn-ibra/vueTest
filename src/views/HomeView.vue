<template lang="">
  <div class="container mt-5">
    <table class="table">
      <thead>
        <tr>
          <th scope="col">No.</th>
          <th scope="col">Nama Kelas</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(k, index) in kelas">
          <th scope="row">{{index+1}}</th>
          <td>{{k.nama_kelas}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import router from '@/router';
import axios from 'axios';

export default {
  data(){
    this.token = localStorage.getItem('token')
    return {
      token: this.token,
      kelas: [],
      no: 0,
    }
  },

  mounted(){
    if(this.token == '' || this.token == null){
      router.push('login');
    }

    axios.get('http://absensmk.prestasiprima.sch.id/api/kelas')
    .then((response) => {
      this.kelas = response.data;
      this.no = 1;
    })
    .catch((error) => {
      console.log(error);
    })
  },
}
</script>
<style lang="">
  
</style>