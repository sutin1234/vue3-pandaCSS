<script setup lang="ts">
import { computed, reactive, ref } from 'vue'
import { css, cva } from '../../styled-system/css'
const myClass = reactive({ fontSize: '5xl', fontWeight: 'bold', p: '2' })
const computedClass = computed(() => css(myClass))
const toggle = ref(false)
const button = cva({
  base: { display: 'flex' },
  variants: {
    visual: {
      solid: { bg: 'red.200', color: 'white' },
      outline: { borderWidth: '1px', borderColor: 'red.200' }
    },
    size: { sm: { padding: '4', fontSize: '12px' }, lg: { padding: '8', fontSize: '24px' } }
  }
})
const handleToggle = () => {
  toggle.value = !toggle.value
  Object.assign(myClass, { color: 'red.500' })
}
</script>

<template>
  <main>
    <div :class="computedClass">Hello 🐼!</div>
    <button
      :class="button({ visual: toggle ? 'outline' : 'solid', size: toggle ? 'sm' : 'lg' })"
      @click="handleToggle"
    >
      Click Me
    </button>
    {{ myClass }}
  </main>
</template>
