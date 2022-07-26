<template>
  <v-app light>

    <Navbar></Navbar>

    <ContentView :show-open-todos="showOpenTodos" />

    <Bottombar
      v-on:show-open-todos="setStatus"
    ></Bottombar>

  </v-app>
</template>

<script>
  import Navbar      from '@/components/Navbar';
  import ContentView from './components/ContentView';
  import Bottombar   from "./components/Bottombar";

  export default {
    name : 'App',

    components : {
      Navbar,
      ContentView,
      Bottombar
    },

    data()
    {
      return { showOpenTodos : true }
    },
    methods : {
      setStatus(value) {
        console.log(value);
        this.showOpenTodos = value;
      }
    }
  };
</script>

<style scoped>
  p{
    font-size : x-large;
  }
</style>
