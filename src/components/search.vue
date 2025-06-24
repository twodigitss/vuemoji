<script setup lang="js">
  import {ref, watch, reactive} from 'vue';
  import emojibase from "../assets/emojibase.json"
  import Emoji from "./emojiGrid.vue"

  const query = ref('')
  const results = ref(emojibase)

  watch(query, value => {
    const filter = emojibase.filter(
      item => item.name.includes(query.value)
    );
    results.value = filter

  })

</script>

<template>
  <p class="search-txt text-base "> 🔎 Search by description </p>
  <input id="query" type="text" v-model="query" placeholder="e.g. flower"
    class="rounded-md duration-150 my-2"
  />
  <Emoji :filteredEmojis="results" />
</template>

<style scoped>
.search-txt{
  margin-top: 0.5rem;
  color: hsl(from var(--body) h s calc(l + 55));
}
#query{
  margin-bottom: 1.5rem;
  padding: 0rem 0.8rem 0rem 0.8rem;
  background-color: hsl(from var(--body) h s calc(l + 1.5));
  &:focus{
    outline: none;
    background-color: hsl(from var(--body) h s calc(l + 2.5));
  }
}
</style>

