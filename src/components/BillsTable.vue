<template>
  <table class="table">
    <thead class="bg-blue-500 text-white">
      <tr>
        <th scope="col">Date</th>
        <th scope="col">Amount</th>
        <th scope="col">Category</th>
        <th scope="col"></th>
      </tr>
    </thead>
    <tbody>
      <tr class="bg-blue-200 text-center">
        <td colspan="4">
          <button class="underline" @click="triggerShowAddBill">Add new bill</button>
        </td>
      </tr>
      <tr v-for="(bill, index) in bills" :key="index">
        <td>{{ bill.date | moment('MMMM D YYYY') }}</td>
        <td>${{ bill.amount }}</td>
        <td>{{ bill.category }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: ['bills'],

  methods: {
    triggerShowAddBill() {
      this.$emit('triggerShowAddBill')
    }
  }
}
</script>
