<template>
  <div>
    <p v-if="$fetchState.pending">Fetching modules...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-else>
      <b>Nuxtjs</b>
      <br>
      <h1>Project Modules:</h1>
      <ul>
        <li v-for="module of modules">{{ module }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import * as https from "https";

  export default {
    data() {
      return {
        modules: []
      }
    },
    async fetch() {
      // NOTE: this is just a basic axios request
      const client = this.$axios.create()
      client.setBaseURL('https://dev-standalone-base.local.host/api')
      const httpsAgent = new https.Agent({
        rejectUnauthorized: false
      });
      
      this.modules = await client.$get('/home', { httpsAgent })
    }
  }
</script>