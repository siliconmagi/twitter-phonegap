<template lang="pug">
  div#app
    f7-views(navbar-through='')
      f7-view(main='', url='/', :dynamic-navbar='true')
        f7-navbar
          f7-nav-left
          f7-nav-center(sliding='') Home
          f7-nav-right
        f7-pages#pages
          f7-page.navbar-fixed
            f7-searchbar(cancel-link='Cancel', placeholder='Search in items', :clear-button='true', v-on:change="onChange")
            f7-list
              f7-list-item(v-for='tweet in tweets', :title='tweet.user.name' link='/page1/')
</template>

<script>
  import cb from './token.js';

  let self;

  export default {
    name: 'app',
    data() {
      return {
        tweets: []
      }
    },
    created() {
      self = this;
    },
    methods: {
      onChange: function(event) {
        let term = event.target.value
        cb.__call(
          "search_tweets",
          "q=" + term,
          function(reply) {
            self.tweets = reply.statuses;
          },
          true // this parameter required
        );
      }
    }
  }
</script>

<style lang="sass?indentedSyntax">
  /* Add your styles here */
</style>
