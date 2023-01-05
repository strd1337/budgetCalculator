<template>
  <div class="budget-list-wrap">
    <ElCard :header="header">
      <template v-if="!isEmpty">
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
          <span class="budget-comment">{{ item.comment }}</span>
          <span class="budget-value">{{ item.value }}</span>
          <ElButton type="danger" size="large" @click="deleteItem(item.id)">Delete</ElButton>
        </div>
      </template>
      <ElAlert v-else type="info" :title="emptyTitle" :closable="false"/>
    </ElCard>
    <ElDialog
      v-model="centerDialogVisible"
      title="Confirmation"
      width="30%"
      centerDialogVisible
    > 
      <span>Are you sure that you want to delete the item?</span>
      <template #footer>
        <span class="dialog-footer">
          <ElButton @click="centerDialogVisible = false">Cancel</ElButton>
          <ElButton type="primary" @click="handleOk(),centerDialogVisible = false">
            Confirm
          </ElButton>
        </span>
      </template>
    </ElDialog>
  </div>
</template>

<script>
export default {
  name: "BudgetList",
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    header: "Budget List",
    emptyTitle: "Empty List",
    centerDialogVisible: false,
    idDeletedItem: 1,
    imgItem: {
      Income: 'Top',
      Outcome: 'Bottom'
    }
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    }
  },
  methods: {
    deleteItem(id) {
      this.centerDialogVisible = true;
      this.idDeletedItem = id;
    },
    handleOk() {
      this.$emit("deleteItem", this.idDeletedItem);
    }
  }
}
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}

.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}

.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}

.dialog-footer button:first-child {
  margin-right: 10px;
}
</style>