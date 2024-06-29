<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>
      <v-form
        v-model="form"
        @submit.prevent="handleSubmit"
      >
        <v-responsive
          class="mx-auto"
          max-width="344"
        >
          <v-text-field v-model="email" label="Email" type="input" variant="solo-filled"></v-text-field>
          <v-text-field v-model="password" label="Password" type="password" variant="solo-filled"></v-text-field>
          <v-btn
            color="success"
            size="large"
            type="submit"
            variant="elevated"
            block
          >
            Sign In
          </v-btn>
        </v-responsive>
      </v-form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  components: {},
  props: {
    msg: String
  },
  data() {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    handleSubmit() {
      const payload = {
        Email: this.email,
        Password: this.password,
        GrantType: this.password,
        Scope: "amazon_data",
        ClientId: "C0001",
        ClientSecret: "SECRET0001",
        RedirectUri: "https://api.eva.guru"
      };
      const headers = {
        'Content-Type': 'application/json',
      };

      axios.post('https://iapitest.eva.guru/oauth/token', payload, { headers })
        .then(response => {
          console.log('Login successful:', response.data);
        })
        .catch(error => {
          console.error('Login failed:', error);
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
