<template>
  <div class="search">
    <input type="text" v-model="query" @keypress.enter="handleSearch" />
    <button @click="handleSearch">Search</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: "",
    };
  },
  methods: {
    handleSearch() {
      this.$emit("SearchRequested", this.query);
      console.log(this.query);
    },
  },
};
</script>