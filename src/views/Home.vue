<template>
  <div class="home">
     <div v-if="loading">
       <h3>Loading...</h3>
     </div>
     <div>
       <news-item v-for="item in items" :key="item.id" :item="item" />
     </div>
  </div>
</template>

<script>
import { value, onCreated } from 'vue-function-api';
import NewsItem from '../components/NewsItem.vue';

const BASE_URL = 'https://api.hackernews.io';

// test

export default {
  components: {
    NewsItem,
  },

  setup() {
    const items = value(new Array([]));
    const loading = value(true);

    onCreated(async () => {
      const response = await fetch(`${BASE_URL}/news?page=1`);
      const json = await response.json();

      items.value = json;
      loading.value = false;
    });

    return {
      items,
      loading,
    };
  },
};

</script>

<style>
.home {
   background-color: #f6f6ef;
}
</style>
