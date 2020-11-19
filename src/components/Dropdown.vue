<template>
  <div class="dropdown" ref="dropdownRef">
    <a
      href="#"
      class="btn btn-outline-light my-2 dropdown-toggle"
      @click.prevent="t"
    >
      {{ title }}
    </a>
    <ul class="dropdown-menu" :style="{ display: 'block' }" v-if="isOpen">
      <slot></slot>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue'
import useClickOutside from '../hooks/useClickOutside'
export default defineComponent({
  name: 'Dropdown',
  props: {
    title: {
      type: String,
      required: true
    }
  },
  setup () {
    const isOpen = ref(false)
    const t = () => {
      isOpen.value = !isOpen.value
    }
    const dropdownRef = ref<null | HTMLElement>(null)
    //   onMounted(() =>{
    //       document.addEventListener('click', handler)
    //   })
    //   onUnmounted(() => {
    //       document.removeEventListener('click', handler)
    //   })
    //   const handler = (e: MouseEvent) => {
    //       if (dropdownRef.value) {
    //           if (!dropdownRef.value.contains(e.target as HTMLElement ) && isOpen.value ) {
    //               isOpen.value = false
    //           }
    //       }
    //   }
    const isClickOutSide = useClickOutside(dropdownRef)

    watch(isClickOutSide, () => {
      if (isOpen.value && isClickOutSide.value) {
        isOpen.value = false
      }
    })
    return {
      isOpen,
      t,
      dropdownRef
    }
  }
})
</script>

<style scoped>
</style>
