<script setup>
import CountdownHeader from '@/components/CountdownHeader.vue'
import CountdownSegment from './components/CountdownSegment.vue'
import { useNow } from '@vueuse/core'
import { computed } from 'vue'
const now = useNow() // useNow gives us the reactive time for every second without having to call setInterval
const year = now.value.getFullYear()

const christmas = new Date(year, 11, 25) // find Christmas for the given year
const one_day = 1000 * 60 * 60 * 24
const one_hour = 1000 * 60 * 60
const one_minute = 1000 * 60
const one_second = 1000

const distance = computed(() => {
  return christmas.getTime() - now.value.getTime()
})

const days = computed(() => {
  return Math.floor(distance.value / one_day)
})

const hours = computed(() => {
  return Math.floor((distance.value % one_day) / one_hour)
})

const minutes = computed(() => {
  return Math.floor((distance.value % one_hour) / one_minute)
})

const seconds = computed(() => {
  return Math.floor((distance.value % one_minute) / one_second)
})

</script>
<template>
  <div class="w-full h-full flex justify-center items-center p-10">
    <div>
      {{now}}
      <div class="shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px]">
        <CountdownHeader />
        <main class="flex justify-center">
          <CountdownSegment label="days" :number="days" />
          <CountdownSegment label="hours" :number="hours" />
          <CountdownSegment label="minutes" :number="minutes" />
          <CountdownSegment label="seconds" :number="seconds" />
        </main>
      </div>
      <h4 class="mt-10 text-gray-400 text-center text-sm">
        This challenge brought to you by <a href="https://vueschool.io/" class="underline">Vue School</a>
      </h4>
    </div>
  </div>
</template>

<style>
div {
  display: block;
}

body {
  @apply bg-gray-100;
}
</style>
