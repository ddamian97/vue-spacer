<template>
  <div :class="[{flexStart: step === 1}, 'wrapper']">
    <transition name="slide">
      <img src="../assets/logo.svg" class="logo" alt="" v-if="step === 1">
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <Item
        v-for="item in results" :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"/>
    </div>
    <div class="loading" v-if="step === 1 && loading"/>
    <ItemModal v-if="modalOpen" @closeModal="modalOpen = false"
    :item="modalItem"/>
  </div>
</template>
<script>
// always use this here in script
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import ItemModal from '@/components/ItemModal.vue';

const API = 'https://images-api.nasa.gov/search';
export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    ItemModal,
  },

  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      // if we have var in v-model it has to have initial val in data
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>
<style lang="scss" scoped>
.wrapper{
  position: relative;
  width: 100%;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  height: 100vh;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
  &.flexStart{
    justify-content: flex-start;
  }
  .fade-enter-active, .fade-leave-active{
    transition: opacity 1s ease;
  }
  .fade-enter, .fade-leave-to{
    opacity: 0;
  }
  .logo{
    position: absolute;
    top: 40px;
    left: 50%;
    transform: translateX(-50%);
  }
  .slide-enter-active, .fade-leave-active{
    transition: margin-top 1s ease;
  }
  .slide-enter, .fade-leave-to{
    margin-top: -50px;
  }
  .results{
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 20px;
    @media (max-width: 768px) {
      grid-template-columns: 1fr 1fr;
    }
  }
  .loading {
    display: inline-block;
    width: 80px;
    height: 80px;
    position: absolute;
    top: 50%;
    left: 50%;
    -webkit-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    z-index: 9;
  }
  .loading:after {
    content: " ";
    display: block;
    width: 64px;
    height: 64px;
    margin: 8px;
    border-radius: 50%;
    border: 6px solid #1e3d4a;
    border-color: #fff transparent #1e3d4a transparent;
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
}
</style>
