<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
    <ul>
      <li v-for="item in results" :key="item.data[0].nasa_id">
        <p>{{ item.data[0].description}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
import Claim from "@/components/Claim.vue";
import SearchInput from "@/components/SearchInput.vue";
const API = "https://images-api.nasa.gov/search";

export default {
  name: "Search",
  components: {
    Claim,
    SearchInput
  },
  data() {
    return {
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleInput: debounce(function() {
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(res => {
          this.results = res.data.collection.items;
        })
        .catch(err => {
          console.log(err);
        });
    }, 500)
  }
};
</script>
<style lang="scss" scoped>
.wrapper {
  margin: 0;
  height: 100vh;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  background-image: url('../assets/dark.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 0%;
}
</style>

