<template>
  <div class="navbar">
    <v-app-bar
      color="blue"
      dark
    >
      <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>

      <v-toolbar-title>TODO App</v-toolbar-title>
    </v-app-bar>

    <v-navigation-drawer
      class="navigation-drawer"
      v-model="drawer"
      absolute
      temporary
    >
      <v-list
        nav
        dense
      >
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-account</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Account</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>

<script>

  export default {
    data : () => ( {
      drawer : false,
      group  : null
    } )
  }
</script>

<style scoped>

  .navbar{
    margin : 0;
  }

  .navigation-drawer{
    height : 100%;

  }
</style>
