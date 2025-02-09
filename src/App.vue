<script setup>
import { ref, computed } from 'vue'

const name = ref('')

const greeting = computed(() => {
  const hour = new Date().getHours()
  if (hour < 12) return 'Good morning'
  if (hour < 18) return 'Good afternoon'
  return 'Good evening'
})
</script>

<template>

  <main class="app">
    <section class="greeting">
      <h2 class="title">
        {{ greeting }}, 
        <input type="text" placeholder="Enter name" v-model="name">
      </h2>
      <p v-if="name">good to see you, {{ name }}!</p>

    </section>

</main>

</template>


