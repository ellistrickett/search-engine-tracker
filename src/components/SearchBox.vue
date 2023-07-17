<template>
    <div>
        <input type="text" v-model="searchTerm" @keyup.enter="handleSearchInput"
            placeholder="Enter your search term and press Enter" />
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            searchTerm: "",
        };
    },
    methods: {
        async handleSearchInput() {
            try {
                const response = await fetch(`https://localhost:7254/api/Search`, {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify({ query: this.searchTerm }),
                });

                const data = await response.json();
                this.$emit("search", data.result);
            } catch (error) {
                console.error("Error while searching:", error.message);
                this.$emit("searchError", "Error occurred during search.");
            }
        },
    },
};
</script>
  
<style>
/* Add any styling here if needed */
</style>
  