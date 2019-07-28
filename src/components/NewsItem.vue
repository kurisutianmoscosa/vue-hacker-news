<template>
    <div class="news-item">
        <p>{{item.title}}</p>
        <p class="news-item-details">{{item.points}}<p>
    </div>
</template>

<script>
export default {
  props: ['item'],
};
</script>

<style scoped>
 .news-item {
     font-size: 0.9em;
 }

 .news-item-details {
     font-size: 0.7em;
 }
</style>
