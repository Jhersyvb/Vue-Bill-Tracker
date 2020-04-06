<template>
  <div class="h-100 w-full flex items-center justify-center font-sans">
    <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
      <div class="mb-4">
        <h1 class="text-4xl mb-2 text-gray-900">Enter a category of bills</h1>
        <p>E.g. 'Electricity' or 'Gas' or 'Internet'</p>
        <div class="flex mt-4">
          <input
            v-model="category"
            placeholder="Add category"
            class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          />
          <button
            class="flex-no-shrink p-2 rounded bg-teal-500 text-white hover:bg-teal-600 focus:outline-none focus:shadow-outline"
            @click="handleClick"
          >
            Add
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      category: ''
    }
  },

  methods: {
    handleClick() {
      if (!this.category) {
        alert('Enter a category')
        return
      }

      this.$emit('addCategory', this.category)
    }
  }
}
</script>
