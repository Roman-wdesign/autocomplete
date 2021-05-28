<template>
  <div class="container">
    <div class="currency"
         v-for="user in users" :key="user.id"
         :id="user.id"
         :name="user.name"
         :username="user.username"
         :email="user.email"
    >
      <p>id: {{user.id}}</p>
      <p>name: {{ user.name }}</p>
      <p>username: {{user.username}}</p>
      <p>email: {{user.email}}</p>

    </div>
  </div>
</template>

<script>

import axios from 'axios'

export default {

  name: 'HelloWorld',

  data: () => ({
    users: [],
    id: Number,
    name: String,
    username: String,
    email: String

  }),
  mounted() {
    axios
        .get('https://jsonplaceholder.typicode.com/users')
        .then(response => (this.users = response.data));

  }
}
</script>
