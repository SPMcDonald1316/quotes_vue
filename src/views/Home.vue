<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="showAllQuotes()">Click here for all quotes</button>
    <button v-on:click="movieQuotes()">Click here for movie quotes</button>
    <button v-on:click="gameQuotes()">Click here for game quotes</button>
    <div v-bind:key="quote.id" v-for="quote in quotes">
      <p>{{ quote.quote }}</p>
      <p>{{ quote.source }}</p>
      <p>{{ quote.context }}</p>
      <p>{{ quote.theme }}</p>
      <hr>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      quotes: [],
    };
  },
  created: function() {
    axios.get("https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json").then(response => {
      this.quotes = response.data;
    });
  },

  methods: {
    showAllQuotes: function() {
      axios.get("https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json").then(response => {
        this.quotes = response.data;
      });
    },
    movieQuotes: function() {
      axios.get("https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json").then(response => {
        this.quotes = response.data.filter(quote => quote.theme === 'movies');
      });
    },
    gameQuotes: function() {
      axios.get("https://gist.githubusercontent.com/benchprep/dffc3bffa9704626aa8832a3b4de5b27/raw/quotes.json").then(response => {
        this.quotes = response.data.filter(quote => quote.theme === 'games');
      });
    }
  }
};
</script>
