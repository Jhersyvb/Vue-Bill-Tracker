<template>
  <div id="app">
    <AddCategory v-if="shouldShowAddCategory" @addCategory="addCategory" />
    <div v-else>
      <AddBill v-if="shouldShowAddBill" :categories="categories" @addBill="addBill" />
      <div v-else>
        <NavBar :categories="categories" @triggerShowAddCategory="triggerShowAddCategory" />
        <div class="container flex">
          <div class="w-1/2">
            <BillsTable :bills="bills" @triggerShowAddBill="triggerShowAddBill" />
          </div>
          <div class="w-1/2">
            <Chart />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AddCategory from './components/AddCategory'
import AddBill from './components/AddBill'
import NavBar from './components/NavBar'
import Chart from './components/Chart'
import BillsTable from './components/BillsTable'

export default {
  name: 'App',

  components: {
    AddCategory,
    AddBill,
    Chart,
    BillsTable,
    NavBar
  },

  data() {
    return {
      bills: [],
      categories: [],
      shouldShowAddCategory: false,
      shouldShowAddBill: false
    }
  },

  watch: {
    bills() {
      localStorage.setItem('bills', JSON.stringify(this.bills))
    },

    categories() {
      localStorage.setItem('categories', JSON.stringify(this.categories))
    }
  },

  mounted() {
    if (localStorage.getItem('bills')) {
      this.bills = JSON.parse(localStorage.getItem('bills'))
    }

    if (localStorage.getItem('categories')) {
      this.categories = JSON.parse(localStorage.getItem('categories'))
    }

    if (!this.bills.length && !this.categories.length) {
      this.shouldShowAddCategory = true
    }
  },

  methods: {
    addCategory(category) {
      this.categories.push(category)
      this.shouldShowAddCategory = false
    },

    triggerShowAddCategory() {
      this.shouldShowAddCategory = true
    },

    addBill(bill) {
      this.bills.push(bill)
      this.shouldShowAddBill = false
    },

    triggerShowAddBill() {
      this.shouldShowAddBill = true
    }
  }
}
</script>
