<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>

    <button v-on:click="createTodo">Create Todo</button>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import { API } from 'aws-amplify';
import { createTodo } from './graphql/mutations';

// const createTodo = `
//   mutation CreateTodo(
//     $input: CreateTodoInput!
//     $condition: ModelTodoConditionInput
//   ) {
//     createTodo(input: $input, condition: $condition) {
//       id
//       name: String!
//       description: String
//     }
//   }
// `

export default {
  name: 'App',
  components: {
    HelloWorld
  },
 data() {
    return {
      name: '',
      description: ''
    }
  },
  methods: {
    async createTodo() {
      // const { name, description } = this;
      // if (!name || !description) return;
      const todo = { name:"Vuue", description:"hello vue" };
      await API.graphql({
        query: createTodo,
        variables: {input: todo},
      });
      // this.name = '';
      // this.description = '';
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
