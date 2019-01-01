<template>
  <div class="heroImage"/>
</template>

<script>
export default {
name: 'HeroImage'
}
</script>

<style lang="scss" scoped>
.heroImage {
  position: fixed;
  top: 0;
  z-index: -1;
  height: 100vh;
  width: 100%;
  background-image: url('../assets/dark.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 0%;
}
.heroImage::after {
  content: '';
  background: rgba($color: #000000, $alpha: 0.2);
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  width: 100%;
  height: 100%;

}
</style>
