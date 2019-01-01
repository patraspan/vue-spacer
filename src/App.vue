

<template>
  <div class="app">
    <!-- <div class="nav">
      <router-link to="/">spacer</router-link>
      <router-link to="/about">about</router-link>
    </div> -->
    <div :class="[{flexStart: step === 1}, 'wrapper']">
      <transition name="slide">
        <img src="./assets/logo.svg" v-if="step === 1" />
      </transition>
      <transition name="fade">
        <HeroImage v-if="step === 0" />
      </transition>
      <Claim v-if="step === 0"/>
      <SearchInput 
      v-model="searchValue"
      @input="handleInput"
      :dark="step === 1"
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
      loading: false,
      step: 0,
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleInput: debounce(function() {
      this.loading = true
      axios
        .get(`${API}?q=${this.searchValue}&media_type=image`)
        .then(res => {
          this.results = res.data.collection.items;
          this.loading = false
          this.step = 1
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

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
.slide-enter-active, .slide-leave-active {
  transition: margin-top .3s ease;
}
.slide-enter, .slide-leave-to /* .fade-leave-active below version 2.1.8 */ {
  margin-top: -50px;
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
 &.flexStart {
   justify-content: flex-start;
 }
}
</style>
