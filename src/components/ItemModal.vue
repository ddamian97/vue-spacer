<template>
<div class="outerWrapper">
  <div class="innerWrapper">
    <div class="photo">
      <img :src="photo" alt="">
    </div>
    <div class="description">
      <h2 class="title">{{ title }}</h2>
      <p class="">
        {{description}}
      </p>
    </div>
  </div>
  <div class="close" @click="$emit('closeModal')"></div>
</div>
</template>

<script>
export default {
  name: 'ItemModal',
  props: {
    item: {
      type: Object,
      required: true,
    },
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
    this.description = this.item.data[0].description.substr(0, 200);
  },
};
</script>

<style scoped lang="scss">
.outerWrapper{
  position: fixed;
  top: 0;
  left: 0;
  background-color: #f6f6f6;
  max-width: 70%;
  height: 60%;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  -webkit-box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
  box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
  @media (max-width: 1024px) {
    max-width: 100%;
    height: 100%;
  }
  .innerWrapper{
    display: flex;
    height: 100%;
    padding: 50px;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    @media (max-width: 1024px) {
      flex-direction: column;

    }
    .photo{
      width: 100%;
      height: auto;
      background-color: black;
      min-width: 50%;
      margin-right: 20px;
      @media (max-width: 1024px){
        min-width: unset;
        margin-right: 0;
      }
      img{
        width: 100%;
        height: auto;
        display: block;
      }
    }
    .title{
      color: #1e3d4a;
    }
    .description{
      width: 100%;
    }
  }
  .close{
    position: absolute;
    width: 30px;
    height: 30px;
    right: 0;
    top: 0;
    padding: 30px;
    cursor: pointer;
    &:before, &:after{
      position: absolute;
      content: '';
      top: 30px;
      right: 20px;
      display: block;
      width: 20px;
      height: 2px;
      background-color: black;
    }
    &:before{
      transform: rotate(45deg);
    }
    &:after{
      transform: rotate(-45deg);
    }
  }
}

</style>
