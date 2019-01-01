<template>
  <div class="claim-wrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">Begin your jurney through our amazing galaxy and discover places You never heard of</p>
    <p class="subclaim">Type anything to start</p>
  </div>
</template>

<script>
export default {
  name: 'Claim'
};
</script>

<style lang="scss" scoped>
.claim-wrapper {
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
text-align: center;
text-shadow: 0px 1px rgba($color: #000000, $alpha: .3);
}

.claim {
  font-size: 50px;
  margin: 0;
  @media screen and (min-width: 768px){
    font-size: 80px;
  }
  @media (min-width: 1024px){
    font-size: 100px;
  }
}
.subclaim {
  margin-top: 15px 0 0 0;
  font-size: 13px;
  font-weight: 300;
  
  @media screen and (min-width: 768px){
    font-size: 17px;
    letter-spacing: 1px;
    width: 500px;
  }
  @media (min-width: 1024px){
    font-size: 19px;
  }
}
</style>
