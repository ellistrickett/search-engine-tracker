<template>
    <SearchBox @search="handleSearch"  @searchError="handleSearchError" />
    <div v-if="searchResult">
      <p>The target url appears at the following positions in Google Search: {{ searchResult }}</p>
    </div>
</template>

<script>
import SearchBox from "@/components/SearchBox.vue"; // Adjust the path based on your folder structure

export default {
  components: {
    SearchBox,
  },
  data() {
    return {
      searchResult: "",
    };
  },
  methods: {
    handleSearch(searchTerm) {
      this.searchResult = searchTerm;
    },
    handleSearchError(errorMessage) {
      this.searchResult = errorMessage;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
