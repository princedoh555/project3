<script setup>
import { ref, computed } from 'vue'

const myArray =ref([])
const name = ref('')
const input_content = ref('')
const input_category = ref(null)


const greeting = computed(() => {
  if(input_content.value.trim() === '' || input_category.value == null){
  const hour = new Date().getHours()
  if (hour < 12) return 'Good morning'
  if (hour < 18) return 'Good afternoon'
  return 'Good evening'
  }

  myArray.value.push({
    content: input_content.value,
    category: input_category.value,
    done: false,
})

  input_content.value = ''
  input_category.value = null
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
    <section class="create-todo">
      <h3>CREATE A TO LIST</h3>
      <form @submit.prevent = "addTodo">
        <h4>What's on your to do list</h4>
        <input type="text" placeholder="e.g, make a video/page" v-model="input_content"/>

        <h4> pick category</h4>
        <div class="options">
          <label>
           <input type="radio" name="category" value="advert" v-model="input_category">
            <span class="bubble advert"></span>
            <div>Advert</div>
        </label>
        <label>
           <input type="radio" name="category" value="indivdual use" v-model="input_category">
           <span class="bubble individual use"></span>
           <div>Individual Use</div>
        </label>
      </div>
        <input type="submit" value="Add To Do" />
     
    </form>      
 </section>

  <section class="todo-list">
    <div v-for="y in myArray" :class="'todo-item ${y.done ?  }'" :key="y">
      <label>
        <input type="checkbox" v-model="y.done"/>
        <span :class="'bubble ${y.category}'"></span>
      </label>
      <div class="todo-content">
        <input type="text" v-model="y.content"/>
      </div>
    </div>

    </section>
</main>

</template>


