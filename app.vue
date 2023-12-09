<template lang="pug">
div
  NuxtLayout
    NuxtPage
    UiVueSonner
</template>

<script setup>
  useSeoMeta({
    ogImage: "/cover.png",
    twitterTitle: "Starter",
    twitterDescription: "Starter repo.",
    twitterImage: "/cover.png",
    twitterCard: "summary_large_image",
  });
</script>