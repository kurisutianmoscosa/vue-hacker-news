<template>
  <div class="home">
     <div v-if="loading">
       <h3>Loading...</h3>
     </div>
     <div>
       <news-item v-for="item in newsItems" :key="item.id" :item="item" />
     </div>
     <div>
       <p class="More" @click="loadMore">More</p>
     </div>
  </div>
</template>

<script>
import { value, onCreated } from 'vue-function-api';
import { useState, useActions } from '@u3u/vue-hooks';

import types from '../types';
import NewsItem from '../components/NewsItem.vue';

export default {
  components: {
    NewsItem,
  },

  setup() {
    const { loading, newsItems } = useState(['loading', 'newsItems']);
    const { GET_NEWS_ITEMS } = useActions([types.GET_NEWS_ITEMS]);
    const currentPage = value(1);

    onCreated(() => {
      GET_NEWS_ITEMS({
        type: 'news',
        page: currentPage.value,
      });
    });

    const loadMore = () => {
      currentPage.value += 1;
      GET_NEWS_ITEMS({
        type: 'news',
        page: currentPage.value,
      });
    };

    return {
      loading,
      newsItems,
      loadMore,
    };
  },
};

</script>

<style>
.home {
  counter-reset: news;
  background-color: #f6f6ef;
  padding: 1em;
}

.More {
  color: #828282
}

</style>
