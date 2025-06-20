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
  <input id="query" type="text" v-model="query"/>
  <span id="log"></span>
  <Emoji :filteredEmojis="results" />
</template>


