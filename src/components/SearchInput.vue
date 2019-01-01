<template>
  <input
    type="text"
    name="search"
    placeholder="e.g. Moon"
    id="search"
    :class="{ dark }"
    :value="value"
    @input="handleChange"
  >
</template>

<script>
export default {
  name: "SearchInput",
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    }
  },
  methods: {
    handleChange(e){
      this.$emit('input', e.target.value)
    }
  }
};
</script>

<style lang="scss" scoped>
input {
  width: 250px;
  flex-direction: column;
  display: flex;
  color: white;
  margin-top: 50px;
  text-align: center;
  font-size: 18px;
  height: 30px;
  border: 0;
  border-bottom: 1px solid white;
  outline: none;
  background: none;
  transition: box-shadow 0.5s ease-out;
  font-weight: 300;
  @media (min-width: 1024px) {
    font-size: 22px;
    font-weight: 400;
    height: 40px;
  }
  &:focus {
    outline: none;
    box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.5);
  }
}
.dark {
  color: #1e3d4a;
  border-bottom: #1e3d4a;
  &:focus {
    outline: none;
    box-shadow: 0 10px 20px -8px rgba(#1e3d4a, 0.2);
  }
}
</style>
