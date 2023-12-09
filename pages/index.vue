<template lang="pug">
.px-6.pt-6
  p.mb-4 Welcome to the homepage 
  UiButton(@click="toast") Button
</template>

<script setup>
const toast = () => {
  useSonner('Toast', {
    description: 'This is a toast message.',
  })
}
</script>