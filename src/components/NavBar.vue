<template>
  <div>
    <ul class="flex justify-center border-b-4">
      <li v-for="category in categories" :key="category" :class="menuItemClass">{{ category }}</li>
      <li @click="triggerShowAddCategory" :class="menuItemClass">➕</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['categories'],

  data() {
    return {
      menuItemClass: ['p-4', 'bg-gray-200', 'hover:bg-gray-400', 'uppercase', 'font-black', 'cursor-pointer']
    }
  },

  methods: {
    triggerShowAddCategory() {
      this.$emit('triggerShowAddCategory')
    }
  }
}
</script>
