<template>
  <input
    type="search"
    placeholder="search users..."
    @input="searchUsers"
    v-model="searchQuery"
  />
  <div class="displaySearchResults">{{ searchQuery }}</div>
</template>

<script>
export default {
  name: "Search",
  props: {
    usersArray: Array,
  },
  data() {
    return {
      searchQuery: "",
    };
  },
  methods: {
    async searchUsers() {
      const filteredUsers = this.usersArray.filter((user) => {
        let searchResults = this.searchQuery.toLowerCase();
        return user.firstName.toLowerCase().includes(searchResults);
      });
      this.$emit("customEvent", filteredUsers);
    },
  },
  emits: ["customEvent"], // Declare the custom event 'customEvent'
};
</script>

<style scoped>

input,
div {
  height: 80px;
  width: 350px;
  padding: 10px 15px;
  border-radius: 50%/180px;
  font-size: 20px;
  border: 1px solid #41b883;
}

input:focus {
  border: 2px solid #41b883;
}

div {
  width: 150px;
  height: 80px;
  overflow: hidden;
}
</style>