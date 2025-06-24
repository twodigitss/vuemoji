<script setup lang="js">
  import {ref, computed, watch} from 'vue'
  import { useToast } from "vue-toastification";
  import emojibase from '../assets/emojibase.json'

  const props = defineProps({
      filteredEmojis: { type: Array, required: false, default: [] }
  })

  const toast = useToast();

  const copyToClipboard = (char) => {
    const txt = document.createElement("textarea")
    txt.innerHTML = char
    navigator.clipboard.writeText(txt.value)
    toast.success("Copied to clipboard!", {
      position: "bottom-right",
      timeout: 2000,
      closeOnClick: true,
      pauseOnFocusLoss: true,
      pauseOnHover: true,
      draggablePercent: 0.6,
      showCloseButtonOnHover: false,
        toastClassName: "toast1",
        containerClassName: "my-container-class",
      hideProgressBar: true,
      closeButton: "button",
      icon: true,
      rtl: false
    });
    return { toast }
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
  <div class="card_container grid grid-cols-15">
    <section v-for="(i) in RenderSelectedEmojis" :key="i">

      <div class="">
        <a  class="card prevent-select text-xl p-2 gap-2 m-1 flex justify-center cursor-pointer rounded duration-150" 
            :title="i.parsed.name" 
            :key="i.parsed.name"
            v-html="i.parsed.htmlCode[0]" 
            @click="copyToClipboard(i.parsed.htmlCode[0])"
          />
      </div>
    </section>
  </div>
</template>

<style>
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
      &:hover{
        background-color: hsl(from var(--body) h s calc(l + 5));
      }
      &:active{
        background-color: var(--accent);
      }
    }

    .Vue-Toastification__toast--success.toast1 {
      border-left: 5px solid hsl(80, 50%, 40%);
      background-color: hsl(from var(--body) h s calc(l + 5));
      font-size: 14px;
      border-radius: 6px;
    }

</style>
