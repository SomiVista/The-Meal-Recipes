<script setup lang="ts">
// import Search from "./components/Search.vue";
// import Card from "./components/Card.vue";
import { ref } from "vue";
const meals = ref<Array<any>>([]);
const searchPherase = ref<string>("");

function getMeals() {
  fetch(
    `https://www.themealdb.com/api/json/v1/1/search.php?s=${searchPherase.value}`
  )
    .then((response) => response.json())
    .then(({ meals }) => (meals.value = meals));
}
</script>

<template>
  <div class="container mx-auto px-4 md:container md:mx-auto">
    <div
      class="min-h-screen bg-gradient-to-tl from-green-400 to-indigo-900 w-full py-16 px-4"
    >
      <div class="flex flex-col items-center justify-center">
        <div class="bg-white shadow rounded w-full p-10 mt-16">
          <div>
            <lable class="text-sm font-medium leading-none text-gray-800">
              Food name:
            </lable>
            <input
              v-model="searchPherase"
              aria-label="enter email adress"
              role="input"
              type="email"
              class="bg-gray-200 border rounded focus:outline-none text-xs font-medium leading-none text-gray-800 py-3 w-full pl-3 mt-2"
            />
          </div>
          <div class="mt-8">
            <button
              @click="getMeals"
              role="button"
              aria-label="create my account"
              class="focus:ring-2 focus:ring-offset-2 focus:ring-indigo-700 text-sm font-semibold leading-none text-white focus:outline-none bg-indigo-700 border rounded hover:bg-indigo-600 py-4 w-full"
            >
              Search
            </button>
          </div>
        </div>
      </div>
    </div>
    <hr />
    <hr />
    <template v-if="meals">
      <div
        v-for="meal in meals"
        :key="meal.id"
        class="mt-8 block rounded-lg bg-white shadow-[0_2px_15px_-3px_rgba(0,0,0,0.07),0_10px_20px_-2px_rgba(0,0,0,0.04)] dark:bg-neutral-700"
      >
        <!-- <div
        class="relative overflow-hidden bg-cover bg-no-repeat"
        data-te-ripple-init
        data-te-ripple-color="light"
      >
        <img class="rounded-t-lg" :src="meal.strMealThumb" alt="" />
        <a :href="meal.strYoutube">
          <div
            class="absolute bottom-0 left-0 right-0 top-0 h-full w-full overflow-hidden bg-[hsla(0,0%,98%,0.15)] bg-fixed opacity-0 transition duration-300 ease-in-out hover:opacity-100"
          ></div>
        </a>
      </div> -->
        <div class="p-6">
          <h5
            class="mb-2 text-xl font-medium leading-tight text-neutral-800 dark:text-neutral-50"
          >
            {{ meal.idMeal }}: {{ meal.strMeal }}
          </h5>
          <p class="mb-4 text-base text-neutral-600 dark:text-neutral-200">
            Ingredient: {{ meal.strIngredient1 }}
          </p>
        </div>
        <hr />
      </div>
    </template>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
