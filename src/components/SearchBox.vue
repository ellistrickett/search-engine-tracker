<template>
    <div>
        <div class="search-box-container">
            <div class="search-box">
                <div class="input-group">
                    <label for="searchPhrase">Search Phrase:</label>
                    <input type="text" v-model="searchPhrase" @keyup.enter="handleSearchInput"
                        placeholder="land registry searches" />
                </div>
                <div class="input-group">
                    <label for="searchPhrase">TargetUrl:</label>
                    <input type="text" v-model="targetUrl" @keyup.enter="handleSearchInput"
                        placeholder="www.example.co.uk" />
                </div>
            </div>
            
        </div>
        <button @click="handleSearchInput">Search</button>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            searchPhrase: "",
            targetUrl: ""
        };
    },
    methods: {
        async handleSearchInput() {
            try {
                if (!this.searchPhrase || !this.targetUrl) {
                    this.$emit("searchError", "Please enter both search terms.");
                    return;
                }

                const response = await fetch(`https://localhost:7254/api/Search`, {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify({ searchPhrase: this.searchPhrase, targetUrl: this.targetUrl }),
                });

                const data = await response.text();
                this.$emit("search", data);
            } catch (error) {
                console.error("Error while searching:", error.message);
                this.$emit("searchError", "Error occurred during search.");
            }
        },
    },
};
</script>
  
<style>
.search-box-container {
  display: flex;
  justify-content: center;
}

.search-box {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

.input-group {
    margin-bottom: 10px;
}

label {
    margin-right: 5px;
}
</style>
  