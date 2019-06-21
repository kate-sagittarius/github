<template>
  <v-toolbar class="header">
    <v-menu bottom left>
      <template v-slot:activator="{ on }">
        <v-btn
          flat
          icon
          color="#fefefe"
          v-on="on"
        >
          <v-icon>menu</v-icon>
        </v-btn>
      </template>

      <v-list>
        <v-list-tile
          v-for="(item, i) in items"
          :key="i"
          @click=""
        >
          <v-list-tile-title>{{ item.title }}</v-list-tile-title>
        </v-list-tile>
      </v-list>
    </v-menu>

    <v-toolbar-title class="header__title">Github viewer</v-toolbar-title>
  </v-toolbar>
</template>

<script>
export default {
    data: () => ({
      items: [
        { title: 'Home' },
        { title: 'Search' },
      ]
    })
}
</script>

<style scoped>
  .header {
    background-color: #BB4430;
    color: #fefefe;
    z-index: 10;
  }
  .header__title {
    font-weight: 500;
  }
</style>
