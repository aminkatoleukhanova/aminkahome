<template>
  <tfoot v-show="dataDisplayed.length > 0">
    <td>Total</td>
    <td>{{ totalAmount }}</td>
    <td>{{ totalPrice }}</td>
  </tfoot>
</template>
<script>
export default {
  name: "TableFooter",
  computed: {
    totalPrice() {
      let s = 0;
      for (let f of this.dataDisplayed) s += f.price * f.amount;
      return s;
    },
    totalAmount() {
      let s = 0;
      for (let f of this.dataDisplayed) s += f.amount;
      return s;
    },
  },
  props: {
    data: Array,
    dataDisplayed: Array,
    dataFiltered: Array,
  },
};
</script>