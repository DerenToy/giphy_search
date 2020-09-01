<template>
  <div id="app">
    <p v-if="isLoading">Loading...</p>
    <search v-on:SearchRequested="handleSearch"></search>
    <preview :gifs="gifs"></preview>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import Preview from "./components/Preview.vue";
export default {
  name: "app",
  data() {
    return {
      gifs: [],
      isLoading: true,
    };
  },
  components: {
    Search: Search,
    Preview: Preview,
  },
  methods: {
    doQuery(url) {
      fetch(url)
        .then((res) => {
          return res.json();
        })
        .then((res) => {
          this.gifs = res.data;
          this.isLoading = false;
        });
    },
    handleSearch(query) {
      this.gifs = [];
      this.isLoading = true;
      const url = `http://api.giphy.com/v1/gifs/search?q=${query}&api_key=dc6zaTOxFJmzC`;
      this.doQuery(url);
    },
  },
  created() {
    const url = "http://api.giphy.com/v1/gifs/trending?api_key=dc6zaTOxFJmzC";
    this.doQuery(url);
  },
};
</script>

<style>
.search {
  text-align: center;
  margin-top: 35px;
}
.search input {
  padding: 10px 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 400px;
}

.search button {
  padding: 5px 15px;
  border: 1px solid #ccc;
  background-color: #4183c4;
  color: #fff;
  font-size: 16px;
  border-radius: 5px;
}
</style>
