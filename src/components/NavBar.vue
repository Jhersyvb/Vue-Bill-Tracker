<template>
  <ul class="flex justify-center bg-white border-b-4">
    <li
      :class="menuItemClass.concat([activeCategory === '' ? 'bg-gray-600' : 'bg-gray-200'])"
      @click="clearActiveCategory"
    >
      All
    </li>
    <li
      v-for="category in categories"
      :key="category"
      :class="menuItemClass.concat([activeCategory === category ? 'bg-gray-600' : 'bg-gray-200'])"
      @click="setActiveCategory(category)"
    >
      {{ category }}
    </li>
    <li @click="triggerShowAddCategory" :class="menuItemClass.concat(['bg-gray-200'])">➕</li>
  </ul>
</template>

<script>
export default {
  props: ['categories', 'activeCategory'],

  data() {
    return {
      menuItemClass: ['p-4', 'hover:bg-gray-400', 'uppercase', 'font-black', 'cursor-pointer']
    }
  },

  methods: {
    triggerShowAddCategory() {
      this.$emit('triggerShowAddCategory')
    },

    clearActiveCategory() {
      this.$emit('clearActiveCategory')
    },

    setActiveCategory(category) {
      this.$emit('setActiveCategory', category)
    }
  }
}
</script>
