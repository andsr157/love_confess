<script setup lang="ts">
import { ref, watch } from "vue"

interface Point {
  x: number
  y: number
}

const position = ref<Point[]>([{ x: 0, y: 0 }])
const isAccept = ref<boolean>(false)

const words = [
  "pleaseeee",
  "pikirkan lagi",
  "aku anaknya presiden lho",
  "mau iphone",
]
const word = ref<string>("")

watch(position, () => {
  generateWord(words)
})

function generateWord(words: string[]) {
  word.value = words[Math.floor(Math.random() * words.length)]
}

function randomPosition() {
  const [currentPosition = { x: 0, y: 0 }, ...rest] = position.value
  let x = Math.floor(Math.random() * 500)
  let y = Math.floor(Math.random() * 500)

  position.value = [{ ...currentPosition, x, y }, ...rest]

  console.log(x)
  console.log(y)
}

function handleAccept() {
  isAccept.value = true
}
</script>

<template>
  <div v-if="isAccept">
    <h1 class="text-4xl text-center pb-2 font-bold text-[#FFEDF9] mt-14">
      Otw Kawin kawanku!!!
    </h1>
  </div>
  <div v-else>
    <h1 class="text-4xl text-center pb-2 font-bold text-[#FFEDF9]">
      Maukah kamu menerima cintaku ?
    </h1>
    <h1 class="text-2xl text-center mb-5 text-[#FFEDF9] font-medium">
      {{ word }}
    </h1>
    <div class="w-56 mx-auto">
      <button
        @click="handleAccept"
        class="bg-[#FE0094] text-bold py-2 px-5 me-4 rounded-md text-white"
      >
        Yes
      </button>
      <button
        @mouseenter="randomPosition"
        class="bg-[#FE0094] relative text-bold py-2 px-5 cursor-default rounded-md text-white"
        :style="{
          top: position[0].y + 'px',
          left: position[0].x + 'px',
        }"
      >
        No
      </button>
    </div>
  </div>
</template>

<style></style>
