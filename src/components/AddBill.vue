<template>
  <div class="h-100 w-full flex flex-col items-center justify-center font-sans">
    <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
      <div class="mb-4">
        <h1 class="text-4xl mb-2 text-gray-900">Enter a new bill</h1>
        <p>E.g. 'Electricity' or 'Gas' or 'Internet'</p>
        <div class="flex mt-4">
          <datepicker v-model="date" class="w-1/3" :input-class="inputClass"></datepicker>
          <div class="w-1/3 inline-block relative">
            <select v-model="category" :class="inputClass">
              <option v-for="category in categories" :value="category" :key="category">{{ category }}</option>
            </select>
            <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
              <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
                <path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z" />
              </svg>
            </div>
          </div>
          <div class="w-1/3">
            <input placeholder="Set amount" v-model="amount" :class="inputClass" />
          </div>
          <button
            class="lex-no-shrink p-2 ml-4 rounded bg-teal-500 text-white hover:bg-teal-600 focus:outline-none focus:shadow-outline"
            @click="handleClick"
          >
            Add
          </button>
        </div>
      </div>
    </div>
    <button class="underline" @click="goBack">Go back</button>
  </div>
</template>

<script>
import Datepicker from 'vuejs-datepicker'

export default {
  name: 'AddBill',

  components: { Datepicker },

  props: ['categories'],

  data() {
    return {
      date: new Date(),
      category: this.categories[0],
      amount: 0,
      inputClass: [
        'shadow',
        'appearance-none',
        'border',
        'rounded',
        'py-2',
        'px-3',
        'text-gray-700',
        'leading-tight',
        'focus:outline-none',
        'focus:shadow-outline',
        'w-full'
      ]
    }
  },

  methods: {
    handleClick() {
      if (!this.date) {
        alert('Enter a date')
        return
      }
      if (!this.amount) {
        alert('Enter an amount')
        return
      }

      this.$emit('addBill', {
        date: this.date,
        category: this.category,
        amount: parseInt(this.amount, 10)
      })
    },

    goBack() {
      this.$emit('goBack')
    }
  }
}
</script>
