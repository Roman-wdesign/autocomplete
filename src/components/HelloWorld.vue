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
         :city="user.address.city"

    >
      <div class="card">
        <p class="card__head" style="font-weight: 600; font-size: 1.5rem;">id: {{ user.id }}</p>
        <p><strong>name</strong>: {{ user.name }}</p>
        <p><strong>username</strong>: {{ user.username }}</p>
        <p><strong>email</strong>: {{ user.email }}</p>

        <h4 style="margin: 30px 0 10px 0">Address</h4>
        <p><strong>street</strong>: {{ user.address.street }}</p>
        <p><strong>suite</strong>: {{ user.address.suite }}</p>
        <p><strong>city</strong>: {{ user.address.city }}</p>
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
    suite: String,
    city: String

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
