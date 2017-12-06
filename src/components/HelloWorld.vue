<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'HelloWorld',
    data () {
      return {
        msg: 'Welcome to Java Faggruppe!'
      }
    },
    mounted () {
      axios.get('http://localhost:8081/hello').then(resp => {
        this.msg = resp.data
      })
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
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
