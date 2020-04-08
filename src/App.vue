<template>
  <div id="app" class="h-screen">
    <AddCategory v-if="shouldShowAddCategory" @addCategory="addCategory" @goBack="shouldShowAddCategory = false" />
    <div v-else>
      <AddBill
        v-if="shouldShowAddBill"
        :categories="categories"
        @addBill="addBill"
        @goBack="shouldShowAddBill = false"
      />
      <div v-else>
        <NavBar
          :categories="categories"
          :active-category="activeCategory"
          @clearActiveCategory="clearActiveCategory"
          @setActiveCategory="setActiveCategory"
          @triggerShowAddCategory="triggerShowAddCategory"
        />
        <div class="container mx-auto flex">
          <div class="w-1/2 bg-blue-100">
            <BillsTable :bills="activeBills" @triggerShowAddBill="triggerShowAddBill" @removeBill="removeBill" />
          </div>
          <div class="w-1/2 p-4 bg-gray-100">
            <Chart :bills="activeBills" />
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
      shouldShowAddBill: false,
      activeCategory: ''
    }
  },

  computed: {
    activeBills() {
      return this.bills
        .filter(bill => (this.activeCategory ? bill.category === this.activeCategory : true))
        .sort((a, b) => (new Date(a.date) < new Date(b.date) ? 1 : -1))
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
    },

    removeBill(index) {
      const billFound = this.activeBills[index]
      const billFoundIndex = this.bills.findIndex(bill => bill === billFound)
      this.bills = this.bills.slice(0, billFoundIndex).concat(this.bills.slice(billFoundIndex + 1, this.bills.length))
    },

    clearActiveCategory() {
      this.activeCategory = ''
    },

    setActiveCategory(category) {
      this.activeCategory = category
    }
  }
}
</script>

<style>
#app {
  background-color: #eee;
}
</style>
