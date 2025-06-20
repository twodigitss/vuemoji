<script setup>
  // import Emoji from "./components/emoji.vue"
  import Search from "./components/search.vue"
  import './global.css'
</script>

<template>
    <span>
      <h1> <strong> 🌱 Emoji Pocket </strong> </h1>
      <p> Brought to you by Gw </p>
    </span>
    <Search/>
</template>

<style global>
    :root{
      --fz: 2rem;
      --accent: hsl(40, 90%, 40%, 20%);
    }
    h1{
        font-size: var(--fz);
    }
    p{
        font-size: calc(var(--fz) - 0.8rem);
        font-weight: 500;
    }
</style>
