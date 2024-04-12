<script setup lang="ts">
import { onErrorCaptured } from 'vue'
import { RouterLink, RouterView } from 'vue-router/auto'
import { ref } from 'vue'
const menuIsOpen = ref(false)


onErrorCaptured((err, instance, info) => {
  console.error('erreur : ', err, '\ninfo : ', info, '\ncomposant : ', instance)
  return true
})
</script>

<template>
  <button aria-controls="mainNav" aria-expanded="true" class="rounded-full border-2 border-red-600 bg-red-300 px-2">
    menu
  </button>
  <header>
    <nav>
      <ul>
        <li>
          <RouterLink to="/" class="text-red-500 underline"> Accueil </RouterLink>
        </li>
        <li>
          <RouterLink to="/accordéon" class="text-red-500 underline"> Accordéon </RouterLink>
        </li>
      </ul>
    </nav>
  </header>
  <RouterView v-slot="{ Component }">
    <Suspense>
      <component :is="Component" />
    </Suspense>
  </RouterView>
</template>
