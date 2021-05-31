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

    <v-card
        color="white"
        style="box-shadow: none !important;"
    >

      <v-card-text>
        <v-autocomplete
            v-model="model"
            :items="items"
            :loading="isLoading"
            :search-input.sync="search"
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
      <v-divider></v-divider>
      <v-expand-transition>
        <v-list
            v-if="model"
            class="red lighten-3"
        >
          <v-list-item
              v-for="(field, i) in fields"
              :key="i"
          >
            <v-list-item-content>
              <v-list-item-title v-text="field.value"></v-list-item-title>
              <v-list-item-subtitle v-text="field.key"></v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-expand-transition>
    </v-card>
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
    descriptionLimit: 60,
    entries: [],
    isLoading: false,
    model: null,
    search: null,

  }),
  computed: {
    fields () {
      if (!this.model) return []

      return Object.keys(this.model).map(key => {
        return {
          key,
          value: this.model[key] || 'n/a',
        }
      })
    },
    items () {
      return this.entries.map(entry => {
        const Description = entry.Description.length > this.descriptionLimit
            ? entry.Description.slice(0, this.descriptionLimit) + '...'
            : entry.Description

        return Object.assign({}, entry, { Description })
      })
    },
  },
  watch: {
    search (val) {
      // Items have already been loaded
      if (this.items.length > 0) return

      // Items have already been requested
      if (this.isLoading) return

      this.isLoading = true

      // Lazily load input items
      axios
            .get('https://jsonplaceholder.typicode.com/users')
            .then(response => (this.users = response.data, console.log(response)))
            .catch(error => this.users = console.log(error))
            .finally(() => console.log('%cData users loading complete', 'background: #0096d3; color: #FFFFFFFF'))
      return val;

    },
  },
  // mounted() {
  //   axios
  //       .get('https://jsonplaceholder.typicode.com/users')
  //       .then(response => (this.users = response.data, console.log(response)))
  //       .catch(error => this.users = console.log(error))
  //       .finally(() => console.log('%cData users loading complete', 'background: #0096d3; color: #FFFFFFFF'))
  //
  // }
}
</script>

<style lang="scss">
.card {
  margin: 5rem 0;
}
</style>