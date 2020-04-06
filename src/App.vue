<template>
  <div id="app">
    <AddCategory v-if="shouldShowAddCategory" @addCategory="addCategory" />
    <div v-else>
      <NavBar />
      <div class="container flex">
        <div class="w-1/2">
          <BillsTable />
        </div>
        <div class="w-1/2">
          <Chart />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AddCategory from './components/AddCategory'
// import AddBill from './components/AddBill'
import NavBar from './components/NavBar'
import Chart from './components/Chart'
import BillsTable from './components/BillsTable'

export default {
  name: 'App',

  components: {
    AddCategory,
    // AddBill,
    Chart,
    BillsTable,
    NavBar
  },

  data() {
    return {
      bills: [],
      categories: [],
      shouldShowAddCategory: false
    }
  },

  watch: {
    categories() {
      localStorage.setItem('categories', JSON.stringify(this.categories))
    }
  },

  mounted() {
    if (localStorage.getItem('categories')) {
      this.categories = JSON.parse(localStorage.getItem('categories'))
    }

    if (!this.categories.length) {
      this.shouldShowAddCategory = true
    }
  },

  methods: {
    addCategory(category) {
      this.categories.push(category)
      this.shouldShowAddCategory = false
    }
  }
}
</script>
