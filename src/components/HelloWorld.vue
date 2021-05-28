<template>
  <div class="container">
    <div class="currency"
         v-for="user in users" :key="user.id"
         :id="user.id"
         :name="user.name"
         :username="user.username"
         :email="user.email"
         :street="user.address.street"
         :suite="user.address.suite"

    >
      <div class="card">
        <p class="head" style="font-weight: 600; font-size: 1.5rem;">id: {{ user.id }}</p>
        <p>name: {{ user.name }}</p>
        <p>username: {{ user.username }}</p>
        <p>email: {{ user.email }}</p>

        <h4 style="margin: 30px 0 10px 0">Address</h4>
        <p>street: {{ user.address.street }}</p>
        <p>suite: {{ user.address.suite }}</p>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'

export default {

  name: 'HelloWorld',

  data: () => ({
    users: [],
    address: [],
    id: Number,
    name: String,
    username: String,
    email: String,
    street: String,
    suite: String

  }),
  mounted() {
    axios
        .get('https://jsonplaceholder.typicode.com/users')
        .then(response => (this.users = response.data))
        .then(response => (this.address = response.data))

  }
}
</script>

<style lang="scss">
.card {
  margin: 5rem 0;
}
</style>
