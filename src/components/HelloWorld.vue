<template>
  <div class="hello">
    <h1>{{ msg }}</h1>    
  </div>
  <div>
    <span>Environment name:</span>
    <input type="text" /> 
  </div>
  <div>
    <span>Location:</span>
    <select>
      <option value="centralus">central us</option>
      <option value="eastus">east us</option>
      <option value="westus">west us</option>
    </select> 
  </div>
  <div>
    <input type="button" value="Create Environment" v-on:click="createOrUpdateEnvironment" /> 
  </div>
    
</template>

<script>
import axios from "axios"

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
        subscriptionId: process.env.VUE_APP_SUBSCRIPTION_ID,
    }
  }, 
  mounted () {
    // GET 
    axios
      .get(`https://management.azure.com/subscriptions/${this.subscriptionId}/resourcegroups?api-version=2020-10-01`)
      .then(response => {
        this.info = response.data.bpi
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  },
  methods: {
    createOrUpdateEnvironment() {
      console.log("create env")
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
