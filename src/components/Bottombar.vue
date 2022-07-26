<template>
  <div class="bottom-bar">
    <v-bottom-navigation color="blue">
      <v-btn class="btn--open-todos" v-on:click="showOpenTodos(true)">
        <span>open todos</span>
        <v-icon>mdi-folder-open-outline</v-icon>
      </v-btn>

      <v-btn class="btn--completed-todos" v-on:click="showOpenTodos(false)">
        <span>completed todos</span>
        <v-icon>mdi-check-all</v-icon>
      </v-btn>
    </v-bottom-navigation>
  </div>
</template>

<script>
export default {
  name: "Bottombar",
  methods: {
    showOpenTodos(show) {
      this.$emit("show-open-todos", show);
    },
  },
};
</script>

<style scoped>
.bottom-bar {
  position: fixed;
  width: 100vw;
  left: 0;
  bottom: 0;
}
</style>
