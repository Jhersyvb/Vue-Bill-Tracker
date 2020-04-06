<template>
  <div id="app">
    <NavBar />
    <div class="container flex">
      <div class="w-1/2">
        <BillsTable />
      </div>
      <div class="w-1/2">
        <Chart :bills="activeBills" />
      </div>
    </div>
  </div>
</template>

<script>
// import AddCategory from './components/AddCategory'
// import AddBill from './components/AddBill'
import NavBar from './components/NavBar'
import Chart from './components/Chart'
import BillsTable from './components/BillsTable'

export default {
  name: 'App',

  components: {
    // AddCategory,
    // AddBill,
    Chart,
    BillsTable,
    NavBar
  }
}
</script>
