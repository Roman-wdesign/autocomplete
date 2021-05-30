<template>
  <div class="container">
    <div class="currency"
         v-for="(user, index) in users" :key="index"
         :id="user.id"
         :name="user.name"
         :username="user.username"
         :email="user.email"
         :street="user.address.street"
         :suite="user.address.suite"
         :city="user.address.city"

         :phone="user.phone"
         :website="user.website"

         :user="user.company.name"
         :catchPhrase="user.company.catchPhrase"

         :zipcode="user.address.zipcode"
         :lat="user.address.geo.lat"
         :lng="user.address.geo.lng"
         :bs="user.company.bs"
    >
      <div class="card">

        <p class="card__head" style="font-weight: 600; font-size: 1.7rem;">id: {{ user.id }}</p>
        <p><strong>name</strong>: {{ user.name }}</p>
        <p><strong>username</strong>: {{ user.username }}</p>
        <p><strong>email</strong>: {{ user.email }}</p>
        <div class="address">

          <h4 style="margin: 30px 0 10px 0; font-size: 1.3rem">Address</h4>
          <p><strong>street</strong>: {{ user.address.street }}</p>
          <p><strong>suite</strong>: {{ user.address.suite }}</p>
          <p><strong>city</strong>: {{ user.address.city }}</p>
          <p><strong>zipcode</strong>: {{ user.address.zipcode }}</p>

          <div class="geo">
            <h4 style="margin: 30px 0 10px 0; font-size: 1.3rem">geo</h4>

            <p><strong>lat</strong>: {{ user.address.geo.lat }}</p>
            <p><strong>lng</strong>: {{ user.address.geo.lng }}</p>
          </div>
          <p><strong>phone</strong>: {{ user.phone }}</p>
          <p><strong>website</strong>: {{ user.website }}</p>

          <div class="company">
            <h4 style="margin: 30px 0 10px 0; font-size: 1.3rem">company</h4>
            <p><strong>name</strong>: {{ user.company.name }}</p>
            <p><strong>catchPhrase</strong>: {{ user.company.catchPhrase }}</p>
            <p><strong>bs</strong>: {{ user.company.bs }}</p>
          </div>
        </div>
      </div>
    </div>
    <template>
      <v-card
          color="white"
          style="box-shadow: none !important;"
      >

        <v-card-text>
          <v-autocomplete
              v-model="value"
              :users="users"
              color="black"
              hide-no-data
              hide-selected
              item-text="Description"
              item-value="API"
              label="Search"
              prepend-icon="mdi-magnify"
              return-object

          ></v-autocomplete>
        </v-card-text>

        </v-card>
    </template>
  </div>
</template>

<script>

import axios from 'axios'

export default {

  name: 'HelloWorld',

  data: () => ({
    users: [],
    address: [],
    geo: [],
    company: [],
    id: Number,
    name: String,
    username: String,
    email: String,
    street: String,
    suite: String,
    city: String,
    zipcode: String,
    lat: String,
    lng: String,
    phone: String,
    website: String,
    catchPhrase: String,
    bs: String,
    value: null
  }),
  mounted() {
    axios
        .get('https://jsonplaceholder.typicode.com/users')
        .then(response => (this.users = response.data, console.log(response)))
        .catch(error => this.users = console.log(error))
        .finally(() => console.log('%cData loading complete', 'background: #505050FF; color: #FFFFFFFF'))
  }
}
</script>

<style lang="scss">
.card {
  margin: 5rem 0;
}
</style>