<template>
  <div class="heroImageWrapper"></div>
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style scoped lang="scss">
.heroImageWrapper{
  position: fixed;
  width: 100%;
  height: 100vh;
  z-index: -1;
  top: 0;
  background-image: url("../assets/heroimage.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 80% 0;
  &:after{
    position: absolute;
    top: 0;
    left: 0;
    content: '';
    z-index: 1;
    width: 100%;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.3);
  }
}
</style>
