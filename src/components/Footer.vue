<template>
  <v-footer class="pa-3 footer" height="68px">
    <v-spacer></v-spacer>
    <div>&copy; {{ new Date().getFullYear() }}</div>
  </v-footer>
</template>

<script>
export default {

}
</script>

<style scoped>
  .footer {
    background-color: #7EBDC2;
    font-weight: 600;
    z-index: 10;
  }
</style>
