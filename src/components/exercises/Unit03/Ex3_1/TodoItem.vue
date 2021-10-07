<template>
  <div class="todo-container">
    <div class="todo-item" v-for="(value, index) in works" :key="index">
      <div class="todo-info">
        <input type="checkbox" @click="choose(index, $event)" :checked="value.isActive">
        <span :class="{ delete: value.isActive }">{{ value.work }}</span>
      </div>
      <button @click="deleteItem(index)" v-if="value.isActive">Xóa</button>
    </div>
    <div class="todo-null" v-if="works.length === 0">
      Chưa có task nào được thêm
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ['todoItem'],
  data() {
    return {
      works: []
    }
  },
  methods: {
    deleteItem(index) {
      this.works.splice(index,1)
    },
    choose(index, event){
      if (event.target.checked) {
        this.works[index].isActive = 1
      } else {
        this.works[index].isActive = 0
      }
    }
  },
  watch: {
    todoItem (value) {
      this.works.push(value)
    }
  }
}
</script>

<style scoped lang="scss">
@import "../../../../assets/scss/Unit03/Ex3_1/todoItem";
</style>