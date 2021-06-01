<template>
  <div class="container">
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
            item-text="name"
            item-value="API"
            label="Search"
            prepend-icon="mdi-magnify"
            return-object
        >

        </v-autocomplete>
      </v-card-text>
      <v-divider></v-divider>
      <v-expand-transition>
        <v-list v-if="model" class="indigo lighten-4">
          <v-list-item
              v-for="(field, name) in fields"
              :key="name"
          >
            <v-list-item-content>
              <v-list-item-title v-text="field.value"
                                 style="color: #0f1d36"
              ></v-list-item-title>

              <v-list-item-subtitle v-text="field.key"
                                    style="color: #1742c2"
              ></v-list-item-subtitle>
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
    idLimit: 60,
    isLoading: false,
    model: null,
    search: null,

  }),
  computed: {
    fields() {
      if (!this.model) return []

      return Object.keys(this.model).map(key => {
        return {
          key,
          value: this.model[key] || 'n/a',
        }
      })
    },
    items() {
      return this.users.map(user => {
        const id = user.id
        const company = user.company.name
        const username = user.username
        const name = user.name
        const email = user.email


        const street = user.address.street
        const suite = user.address.suite
        const city = user.address.city
        const zipcode = user.address.zipcode

        const lat = user.address.geo.lat
        const lng = user.address.geo.lng

        const phone = user.phone
        const website = user.website

        const catchPhrase = user.company.catchPhrase
        const bs = user.company.bs


        return Object.assign({id}, {name}, {username}, {email}, {street}, {suite}, {city}, {zipcode},
            {lat}, {lng}, {phone}, {website}, {company}, {catchPhrase}, {bs})
      })
    },
  },
  watch: {
    search(val) {
      // Items have already been loaded
      if (this.items.length > 0) return

      // Items have already been requested
      if (this.isLoading) return

      this.isLoading = true

      // Lazily load input items
      axios.get('https://jsonplaceholder.typicode.com/users')
          .then(response => (this.users = response.data, console.log(response)))
          .catch(error => this.users = console.log(error, 'Data users error', 'background: #EF1919FF; color: #FFFFFFFF'))
          .finally(() => console.log('%cData users loading complete', 'background: #0096d3; color: #FFFFFFFF'))
      axios.get('https://jsonplaceholder.typicode.com/photos')
          .then(response => (this.photos = response.data, console.log(response)))
          .catch(error => this.photos = console.log(error, 'Data photos error', 'background: #EF1919FF; color: #FFFFFFFF'))
          .finally(() => console.log('%cData photos loading complete', 'background: #1742c2; color: #FFFFFFFF'))
      return val;
    },
  },
}
</script>

<style lang="scss">
.card {
  //color: #ef1919;
  margin: 5rem 0;
}
</style>