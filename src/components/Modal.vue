<template>
  <div class="outer-wrapper">
    <div class="close" @click="$emit('closeModal')"></div>
    <div class="inner-wrapper">
      <div class="photo">
        <img :src="photo" :alt="title">
      </div>
      <div class="desc">
        <h2 class="title">{{title}}</h2>
        <p
          class="description"
        >{{description}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    item: {
      type: Object,
      required: true,
    }
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description;
  }
};
</script>

<style lang="scss" scoped>
.outer-wrapper {
  color: #1e3d4a;
  background: #f6f6f6;
  height: 100%;
  max-width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  @media (min-width: 1024px) {
    max-width: 70%;
    height: 60%;
    left: 0;
    bottom: 0;
    top: 0;
    right: 0;
    margin: auto;
    box-shadow: 0 30px -10px rgba(0, 0, 0, 0.3);
  }
}
.close {
  position: absolute;
  width: 30px;
  height: 30px;
  padding: 20px;
  top: 10px;
  right: 10px;
  cursor: pointer;
  &::before,
  &::after {
    content: "";
    position: absolute;
    top: 20px;
    right: 10px;
    width: 20px;
    height: 2px;
    background: black;
    display: block;
  }
  &::before {
    transform: rotate(45deg);
  }
  &::after {
    transform: rotate(-45deg);
  }
}
.inner-wrapper {
  display: flex;
  height: 100%;
  padding: 50px;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  @media (min-width: 1024px) {
    flex-direction: row;
    .photo {
      width: 50%;
      margin-right: 20px;
    }
  }
  .photo {
    width: 90%;
    height: auto;
    background: black;
    img {
      width: 100%;
    }
  }
  .description {
    max-height: 200px;
    overflow-y: scroll;
  }
}
</style>
