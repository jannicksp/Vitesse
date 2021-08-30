<template>
  <main class="text-center text-gray-700 dark:text-gray-200">
    <Header />
    <router-view />
    <div class="mt-5 mx-auto text-center text-sm">
      [Beer Layout]
    </div>
    <div class="list-container">
      <div class="div-list" v-for="beer in beers" :key="beer.id">
        <p>{{ beer.name }}</p>
        <p> {{ beer.brewery_type }}</p>
        <p>From: {{ beer.city }}, {{ beer.state }}, {{ beer.country }}</p>
        <p> {{beer.website_url}}</p>  
      </div>
    </div>
    <Footer />
  </main>
</template>

<script lang="ts">

export default {
  data() {
    return {
      beers: [],
    }
  },
  created() {
    this.getData()
  },

  methods: {
    async getData() {
      try {
        const response = await fetch('https://api.openbrewerydb.org/breweries')
        this.beers = await response.json()
      }
      catch (error) {
        console.log(error)
      }
    },

  },
}
</script>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}

.list-container{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.div-list{
  background: lightgrey;
  width:300px;
  margin: 10px;
  padding: 25px;
}

.div-list p{
  color:black
  
}

</style>
