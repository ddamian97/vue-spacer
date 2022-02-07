<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input
        type="text"
        id="search"
        name="search"
        v-model="searchValue"
        @input="handleInput"
      >
      <ul>
        <li v-for="item in results" :key="item.data[0].nasa_id">
          <p>{{ item.data[0].description }}</p>

        </li>
      </ul>
      <div></div>
    </div>
  </div>
</template>
<script>
// always use this here in script
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';
export default {
  name: 'Search',
  data() {
    return {
      // if we have var in v-model it has to have initial val in data
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          console.log(this.results);
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
  align-items: center;
  margin: 0;
  padding: 30px;
  .search{
    display: flex;
    flex-direction: column;
    width: 300px;
    label{
      font-family: Montserrat, sans-serif;
    }
    input{
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
    }
  }
}
</style>
