<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input type="text" name="search" id="search" v-model="searchValue" @input="handleInput">
    </div>
    <ul>
      <li v-for="item in results" :key="item.data[0].nasa_id">
        <p>
          {{ item.data[0].description}}
        </p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
const API = "https://images-api.nasa.gov/search";

export default {
  name: "Search",
  data() {
    return {
      searchValue: "",
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function() {
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(res => {
          this.results = res.data.collection.items
        })
        .catch(err => {
          console.log(err);
        });
    },500 )
  }
};
</script>
<style lang="scss" scoped>
.wrapper {
  margin: 0;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}
.search {
  width: 250px;
  flex-direction: column;
  display: flex;
  label {
    font-family: Montserrat, sans-serif;
  }
  input {
    height: 30px;
    border: 0;
    border-bottom: 1px solid black;
    outline: none;
  }
}
</style>

