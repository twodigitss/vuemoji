<script setup>
  import Search from "./components/search.vue"
  import './global.css'
</script>

<template>
    <span class="grid justify-center">
      <h1> <strong> 🌱 Emoji Pocket </strong> </h1>
      <h2 class="font-medium text-base"> Brought to you by Gw (twodigitss)</h2>
      <p > Just the essential emojis for most use cases.
      </p>
      <br/>
    </span>
    <Search/>
</template>

<style scoped>
  br{
    margin-top: 1rem;
  }
  h1{
    font-size: var(--fz);
  }
</style>
