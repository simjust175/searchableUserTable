<template>
  <div class="container">
    <header>
      <img
        id="vueLogo"
        alt="Vue logo"
        src="https://vuejs.org/images/logo.png"
      />
      <Search :users-array="usersArray" @customEvent="searchResults" />
    </header>

    <table>
      <thead>
        <tr>
          <th><h2>Name</h2></th>
          <th><h2>Email</h2></th>
          <th><h2>Phone</h2></th>
          <th><h2>Address</h2></th>
          <th><h2>age</h2></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in searchedArray" :key="index">
          <td>{{ user.firstName }} {{ user.lastName }}</td>
          <!-- <button type="button" @click="isHidden = ''" :class="{hidden: !isHidden}">More info</button> -->
          <span :class="{hidden: isHidden}"></span>
            <td>{{ user.email }}</td>
            <td>{{ user.phone }}</td>
            <td>{{ user.address.address }}</td>
            <td>{{ user.age }}</td>
          
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Search from "./components/icons/Search.vue";
export default {
  components: {
    Search,
  },
  data() {
    return {
      usersArray: [],
      searchedArray: [],
      isHidden: "hidden"
    };
  },
  methods: {
    async fetchUsers() {
      const res = await fetch("https://dummyjson.com/users");
      const { users } = await res.json();
      this.usersArray = users;
      this.searchedArray = users;
    },

    searchResults(query) {
      this.searchedArray = query;
    },
  },
  mounted() {
    this.fetchUsers();
  },
};
</script>

<style>
:root{
  --vue-color:#41b883; 
}
.hidden {
  display: none;
}
.container {
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
}

header {
  align-items: center;
  margin-bottom: 40px;
  display: flex;
  justify-content: space-around;
}

th {
  border-bottom: 2px solid var(--vue-color);
  color: #999;
  cursor: default;
}

td {
  border-top: #999 1px solid;
  padding: 10px 15px;
}

tbody tr:hover {
  cursor: pointer;
  background: #ddd;
}
table {
  border-collapse: collapse;
  width: 100%;
  border-bottom: #999 1px solid;
}

td,
th {
  text-align: left;
}

button{
  border-radius: 6px;
  padding: 0.2rem 0.5rem;
  background-color: var(--vue-color);
  border: 0.5px solid #0af189;
}
#vueLogo {
  height: 100px;
  margin-top: 10px;
}
</style>
