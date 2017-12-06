<template>
  <div class="hello">
    <h1>People</h1>
    <div>
      <input v-model="name" type="text">
      <button v-on:click="submit()">Add Person</button>
    </div>
    <div>
      <ul>
        <li v-for="person in people">{{ person.name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'People',
    data () {
      return {
        name: '',
        people: []
      }
    },
    methods: {
      submit () {
        console.log('created: ' + this.name)
        const person = {name: this.name}
        axios.post('http://localhost:8081/addperson', person).then(resp => {
          console.log('created: ' + JSON.stringify(resp.data))
          this.getPeople()
        })
      },
      getPeople () {
        axios.get('http://localhost:8081/people').then(resp => {
          this.people = resp.data
        })
      }
    },
    mounted () {
      axios.get('http://localhost:8081/hello').then(resp => {
        this.msg = resp.data
      })
      this.getPeople()
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
