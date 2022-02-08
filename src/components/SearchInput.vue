<template>
    <input
      type="text"
      id="search"
      name="search"
      :class="{ dark }"
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
    dark: {
      type: Boolean,
      default: false,
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
    flex-shrink: 0;
    margin-top: 50px;
    width: 400px;
    height: 60px;
    color: #ffffff;
    text-align: center;
    font-size: 22px;
    border: 0;
    background: none;
    border-bottom: 1px solid #ffffff;
    transition: border-color .5s;
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;
    &:focus{
      outline: none;
      border-color: #000000;
    }
  }
  .dark{
    background-color: rgba(0, 0, 0, 0.1);
    color: #000000;
  }
</style>
