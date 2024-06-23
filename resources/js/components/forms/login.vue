<template>
  <div>
    <b-table striped hover :items="items" :fields="fields"></b-table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      items: null,
      fields: ['id', 'USERNAME'],
      form: {
        email: '',
        password: ''
      },
      loading: false
    };
  },
  methods: {
    register() {
      this.loading = true;
      axios.post('/register/registration', this.form).then(response => {
        console.log(response.data.email);
        console.log(response.data.password);
        this.loading = false;
      }).catch(error => {
        console.log(error);
        this.loading = false;
      });
    },
    get_accounts() {
      axios.get('/get_accounts').then(response => {
        console.log(response.data);
        this.items = response.data;
      }).catch(error => {
        console.log(error);
      });
    },
  },
  beforeMount() {
    this.get_accounts();
  }
};
</script>
