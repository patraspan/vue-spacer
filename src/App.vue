

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
      <div class="results" v-if="results && !loading && step === 1">
        <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
      </div>
      <div class="loader" v-if="step === 1 && loading"/>
      <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
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
import Item from "@/components/Item.vue";
import Modal from "@/components/Modal.vue";
//Api 
const API = "https://images-api.nasa.gov/search";

export default {
  name: "App",
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
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
    }, 500),
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item
    }
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

.logo {
  position: absolute;
  top: 30px;
}

.results {
  margin-top: 50px;
  width: 80%;
  display: grid;
  grid-template-columns: 1fr;
  grid-gap: 20px;
  @media (min-width: 500px) {
    grid-template-columns: 1fr 1fr;
  }
  @media (min-width: 768px) {
    grid-template-columns: 1fr 1fr 1fr;
  }
}

.loader {
  display: block;
  width: 64px;
  height: 64px;
  margin-top: 100px;
@media (min-width: 768px) {
    width: 90px;
  height: 90px;
  }

}
.loader:after {
  content: " ";
  display: block;
  width: 46px;
  height: 46px;
  margin: 1px;
  border-radius: 50%;
  border: 5px solid #1e3d4a;
  border-color: #1e3d4a transparent #1e3d4a transparent;
  animation: loading 1.2s linear infinite;
}
@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
