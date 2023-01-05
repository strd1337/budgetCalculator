<template>
  <OperationForm @submitOperationForm="onSubmitOperationForm" />
  <TotalBalance :total="totalBalance"/>
  <div id="app">
    <BudgetList :list="list" @deleteItem="onDeleteItem"></BudgetList>
  </div>
</template>

<script>

import BudgetList from './components/BudgetList.vue';
import TotalBalance from './components/TotalBalance.vue';
import OperationForm from './components/OperationForm.vue';

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    OperationForm
  },
  data: () => ({
    list: [
      {
        type: 'Income',
        value: 40,
        comment: 'Some comment',
        id: 1
      },
      {
        type: 'Outcome',
        value: -25,
        comment: 'Some outcome comment',
        id: 2
      }
    ]
  }),
  methods: { 
    onDeleteItem(id) {
      const filteredList = this.list.filter(element => { return element.id != id; });
      this.list = filteredList;
    },
    onSubmitOperationForm(data) {
      data.id = String(Math.random());
      this.list.push(data);
    }
  },
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => acc + item.value, 0); 
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
