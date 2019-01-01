

<template>
  <div class="app">
    <!-- <div class="nav">
      <router-link to="/">spacer</router-link>
      <router-link to="/about">about</router-link>
    </div> -->
    <div class="wrapper">
      <HeroImage />
      <Claim/>
      <SearchInput 
      v-model="searchValue"
      @input="handleInput"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";
//components
import Claim from "@/components/Claim.vue";
import HeroImage from "@/components/HeroImage.vue";
import SearchInput from "@/components/SearchInput.vue";
//Api 
const API = "https://images-api.nasa.gov/search";

export default {
  name: "App",
  components: {
    Claim,
    SearchInput,
    HeroImage
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

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800");
* {
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
body {
  font-family: "Montserrat", sans-serif;
  margin: 0;
  padding: 0;
}
.wrapper {
  margin: 0;
  min-height: 100vh;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
 color: white;
}
</style>
