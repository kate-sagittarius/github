<template>
  <div class="my-stats__wrapper">
    <v-card class="my-stats">
      <v-list two-line subheader class="my-stats__list">
        <v-subheader>My repositories</v-subheader>
        <v-list-tile
          v-for="item in items"
          :key="item.id"
        >
          <v-list-tile-content>
            <v-list-tile-title>{{ item.name }}</v-list-tile-title>
            <v-list-tile-sub-title><a href="item.svn_url" blank="_target" rel="noopener">{{ item.svn_url }}</a></v-list-tile-sub-title>
          </v-list-tile-content>

          <v-list-tile-action>
            <v-icon color="grey lighten-1">star</v-icon>
          </v-list-tile-action>
        </v-list-tile>
        <div class="my-stats__load-button-wrapper">
          <v-btn 
            outline 
            color="#231F20" 
            v-on:click="reload()"
            :disabled="last===true"
          >
            Outline Button
            <v-icon color="#231F20" class="load-button__icon">sync</v-icon>
          </v-btn>
        </div>
      </v-list>
    </v-card>  
  </div>
</template>

<script>
import axios from 'axios';
import parseLinkHeader from 'parse-link-header';

export default {
  data () {
    return {
      items: [],
      nextLink: '',
      lastLink: '',
      last: false
    }
  },

  mounted() {
    axios
      .get(`https://api.github.com/users/kate-sagittarius/repos?page=1&per_page=5`)
      .then(response => {
        this.items = response.data;
        this.nextLink = parseLinkHeader(response.headers.link).next.url;
        console.log(response);
      })  
  },
  methods: {
    reload() {
      axios
        .get(`${this.nextLink}`)
        .then(response => {
          this.items = [...this.items, ...response.data];

          if (response.headers.link.includes('rel="next"')) {
            this.nextLink = parseLinkHeader(response.headers.link).next.url;
          } else {
            this.last = true;
          }
        })  
    }
  }
}
</script>

<style scoped>
  .my-stats__wrapper, .my-stats, .my-stats__list {
    min-height: calc(100vh - (64px + 68px));
    background-color: #EFE6DD;
  }
  .my-stats {
    padding: 0 24px;
  }
  .my-stats__load-button-wrapper {
    margin-top: 24px;
    display: flex;
    justify-content: center;
  }
  .load-button__icon {
    margin-left: 10px;
  }
</style>
