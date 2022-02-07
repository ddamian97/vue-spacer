<template>
  <div class="wrapper">
    <Claim />
    <SearchInput v-model="searchValue" @input="handleInput"/>
    <HeroImage />
  </div>
</template>
<script>
// always use this here in script
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';

const API = 'https://images-api.nasa.gov/search';
export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    HeroImage,
  },

  data() {
    return {
      // if we have var in v-model it has to have initial val in data
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
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
  width: 100%;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  height: 100vh;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
}
</style>
