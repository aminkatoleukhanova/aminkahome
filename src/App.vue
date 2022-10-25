<template>
  <div id="app">
    <h1>LIST OF FRUITS</h1>
    <br />
    <button class="btn btn-danger" @click="deleteSelected()">
      DELETE SELECTED
    </button>
    <br />
    <br />
    <button class="btn btn-primary" @click="logSelected()">
      LOG SELECTED ON CONSOLE
    </button>
    <br />
    <data-table v-bind="tableProps" />
  </div>
</template>

<script>
import fruits from "./data.js";
import EventBus from "./EventBus.js";
import CustomCheckbox from "./components/CustomCheckbox";

/* add handler to toggle selected fruits for mass-selection */
EventBus.listen("setSelected", function (id, checked) {
  /* very lazy, inefficient searching. But performance
   * is not a concern for the purpose we have here
   */
  for (let i = 0; i < fruits.length; i += 1) {
    if (fruits[i].id === id) {
      fruits[i].selected = checked;
    }
  }
});

export default {
  name: "App",
  data() {
    return {
      tableProps: {
        data: fruits,
        columns: [
          { key: "", sortable: false, component: CustomCheckbox },
          { key: "product" },
          { key: "price", type: "number" },
          { key: "amount", type: "number" },
        ],
      },
    };
  },
  methods: {
    deleteSelected() {
      this.tableProps.data = this.tableProps.data.filter((f) => !f.selected);
    },
    logSelected() {
      console.log(
        this.tableProps.data
          .filter((f) => f.selected)
          .map((o) => {
            return { ...o };
          })
      );
    },
  },
};
</script>

<style>
body {
  padding: 16px 64px;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0 auto;
  max-width: 800px;
}
</style>
