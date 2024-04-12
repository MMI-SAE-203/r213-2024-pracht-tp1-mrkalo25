<script setup lang="ts">
import { onErrorCaptured, vShow } from 'vue'
import { RouterLink, RouterView } from 'vue-router/auto'
import { ref } from 'vue'
const menuIsOpen = ref(false)



onErrorCaptured((err, instance, info) => {
  console.error('erreur : ', err, '\ninfo : ', info, '\ncomposant : ', instance)
  return true
})
</script>

<template>
  <button aria-controls="mainNav" aria-expanded="true" class="rounded-full border-2 border-red-600 bg-red-300 px-2"
    @pointerdown="menuIsOpen = !menuIsOpen">
    menu
  </button>
  <header>
    <Transition class="transition-transform duration-1000" enter-from-class="-translate-x-full"
      enter-to-class="translate-x-0" leave-active-class="-translate-x-full">
      <nav v-show="menuIsOpen">
        <ul>
          <li>
            <RouterLink to="/" class="text-red-500 underline"> Accueil </RouterLink>
          </li>
          <li>
            <RouterLink to="/accordéon" class="text-red-500 underline"> Accordéon </RouterLink>
          </li>
        </ul>
      </nav>
    </Transition>
  </header>
  <RouterView v-slot="{ Component }">
    <Suspense>
      <component :is="Component" />
    </Suspense>
  </RouterView>
</template>
