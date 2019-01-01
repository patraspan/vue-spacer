<template>
  <div class="search-wrapper">
      <input 
        type="text" 
        name="search" 
        placeholder="e.g. Moon"
        id="search" 
        v-model="searchValue" 
        @input="handleInput"
      />
    </div>
</template>

<script>
export default {
name: 'SearchInput'
}
</script>

<style lang="scss" scoped>
.search-wrapper {
  width: 250px;
  flex-direction: column;
  display: flex;
  input {
    margin-top: 50px;
    text-align: center;
    height: 30px;
    border: 0;
    border-bottom: 1px solid black;
    outline: none;
    background: none;
  }
}
</style>
