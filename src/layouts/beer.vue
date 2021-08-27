<template>
  <main class="text-center text-gray-700 dark:text-gray-200">
    <Header />
    <router-view />
    <div class="mt-5 mx-auto text-center opacity-25 text-sm">
      [Beer Layout]
    </div>
    <div class="list-container">
      <h1>test</h1>
      <ul v-for="beer in beers" :key="beer.id">
        <p>{{ beer.name }}</p>
        <p> {{ beer.brewery_type }}</p>
        <p>From: {{ beer.city }}, {{ beer.state }}, {{ beer.country }}</p>
      </ul>
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
ul{
  background: grey;
  width:300px;
  margin: 10px;
  padding: 25px;
}

</style>
