<script setup>
import { ref } from 'vue'

const P1_imgUrl = ref(new URL("../assets/1.jpg", import.meta.url).href)
const P2_imgUrl = ref(new URL("../assets/2.jpg", import.meta.url).href)

const p1_score = ref(0);
const p2_score = ref(0);

function start() {
  const rd1 = Math.floor(Math.random()*3) + 1;
  const rd2 = Math.floor(Math.random()*3) + 1;

  P1_imgUrl.value = new URL("../assets/"+rd1+".jpg", import.meta.url).href
  P2_imgUrl.value = new URL("../assets/"+rd2+".jpg", import.meta.url).href

  if (
    (rd1 == 1 && rd2 == 3) ||
    (rd1 == 2 && rd2 == 1) ||
    (rd1 == 3 && rd2 == 2)
  ) {
    p1_score.value += 1;
  } else if (rd1 != rd2) {
    p2_score.value += 1;
  }
}

function reset() {
  p1_score.value = 0;
  p2_score.value = 0;
}

const count = ref(0)
</script>

<template>
  <div class="bg-gray-800 h-full text-white flex flex-col items-center gap-y-4 p-8">
    <div class="flex flex-row gap-x-8 items-center h-60 p-8">
      <div class="w-56">
        <img class="rounded-md object-fit" :src=P1_imgUrl alt="">
      </div>
      <div class="w-56">
        <img class="rounded-md object-scale-down" :src=P2_imgUrl alt="">
      </div>
    </div>

    <div>
      Scoreboard {{ p1_score }} : {{ p2_score }}
    </div>

    <div class="flex flex-row gap-x-4">
      <button @click="start()" class="bg-slate-500 p-4 rounded-md active:bg-red-600">Start</button>
      <button @click="reset()" class="bg-slate-500 p-4 rounded-md active:bg-red-600">Reset</button>
    </div>
    
  </div>
</template>
