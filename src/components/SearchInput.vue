<template>
    <input
      type="text"
      id="search"
      name="search"
      :value="value"
      @input="handleChange"
    >
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style scoped lang="scss">
  input{
    margin-top: 50px;
    width: 300px;
    height: 30px;
    color: #ffffff;
    text-align: center;
    font-size: 18px;
    border: 0;
    background: none;
    border-bottom: 1px solid #ffffff;
    transition: border-color .5s;
    &:focus{
      outline: none;
      border-color: #000000;
    }
  }
</style>
