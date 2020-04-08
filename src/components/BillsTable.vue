<template>
  <table class="table w-full">
    <thead class="bg-blue-500 text-white">
      <tr>
        <th class="p-4" scope="col">Date</th>
        <th class="p-4" scope="col">Amount</th>
        <th class="p-4" scope="col">Category</th>
        <th class="p-4" scope="col"></th>
      </tr>
    </thead>
    <tbody>
      <tr class="bg-blue-200 text-center">
        <td class="p-4" colspan="4">
          <button class="underline" @click="triggerShowAddBill">Add new bill</button>
        </td>
      </tr>
      <tr v-for="(bill, index) in bills" :key="index">
        <td class="p-4">{{ bill.date | moment('MMMM D YYYY') }}</td>
        <td class="p-4">${{ bill.amount }}</td>
        <td class="p-4">{{ bill.category }}</td>
        <td class="p-4"><button @click="removeBill(index)">𝗫</button></td>
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
    },

    removeBill(index) {
      this.$emit('removeBill', index)
    }
  }
}
</script>
