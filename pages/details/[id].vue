<template>
  <div class="details">
    <img :src="productDetails.thumbnail" :alt="productDetails.title">
    <h2>
      {{ productDetails.title }}
    </h2>
    <div>
      {{ productDetails.description }}
    </div>
  </div>
</template>

<script setup lang="ts">
const route = useRoute();
const itemId = route.params.id

const productDetails = await fetch(`https://dummyjson.com/products/${itemId}`).then(res => res.json()).then(data => data);
const title = `${productDetails.title} | ${productDetails.description}`;

useServerSeoMeta({
  ogTitle: () => title,
  title: () => title,
  description: () => productDetails.description,
  ogDescription: () => productDetails.description,
  ogImage: () => productDetails.thumbnail,
  ogImageUrl: () => productDetails.thumbnail,
  twitterCard: () => 'summary_large_image',
  twitterTitle: () => title,
  twitterDescription: () => productDetails.description,
  twitterImage: () => productDetails.thumbnail
})
</script>

<style>
.details {
  margin: 0 auto;
  text-align: center;
  background-color: antiquewhite;
  padding: 10px;
}
</style>
