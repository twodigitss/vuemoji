<script setup lang="js">
  import {ref, computed, watch} from 'vue'
  import emojibase from '../assets/emojibase.json'
  const props = defineProps({
      filteredEmojis: { type: Array, required: false, default: [] }
  })

  const newCategory = ref('smileys and people')
  watch(newCategory, value => {
    console.log("Valor de newCategory; ", value)
  })

  const check = (currentCat) => {
    if (newCategory.value != currentCat){
      newCategory.value = currentCat
      return true
    }
    return false
  }

  const copyToClipboard = (char) => {
    const txt = document.createElement("textarea")
    txt.innerHTML = char
    navigator.clipboard.writeText(txt.value)
  }

  const RenderSelectedEmojis = computed(() => {
    const collection = props.filteredEmojis || emojibase;
    const group = []

    collection.forEach(emoji => {
      const parsed = JSON.parse(JSON.stringify(emoji))
      group.push({ parsed })
    })
    return group //array
  })


</script>

<template>
  <div class="emoji-container grid grid-cols-15 mt-8">
    <section v-for="(i) in RenderSelectedEmojis" :key="i">

      <span v-if="check(i.parsed.category)">
        <p class="text-lg"> &bull; {{i.parsed.category}}</p>
        <hr class="my-2 border-gray-900"/>
      </span>

      <div class="card p-2 gap-2 m-1 flex justify-center cursor-pointer rounded border duration-250">
        <a  class="emoji-item prevent-select text-xl" 
            :title="i.parsed.name" 
            :key="i.parsed.name"
            v-html="i.parsed.htmlCode[0]" 
            @click="copyToClipboard(i.parsed.htmlCode[0])"
        />
      </div>

    </section>
  </div>
</template>

<style scoped>
    .prevent-select {
        -webkit-user-select: none; /* Safari */
        -ms-user-select: none; /* IE 10 and IE 11 */
        user-select: none; /* Standard syntax */
    }

    hr{
        border-color: hsl(from var(--body) h s calc(l + 15));
    }

    .card{
      background-color: hsl(from var(--body) h s calc(l + 1.5));
      border-color: hsl(from var(--body) h s calc(l + 15));

      &:hover{
        background-color: hsl(from var(--body) h s calc(l + 5));
        /* box-shadow: 1px 2px 2px hsl(0,0%,0%,30%); */
      }

      &:active{
        background-color: var(--accent);
        border-color: hsl(from var(--accent) h s calc(l + 20));
      }
    }

</style>
