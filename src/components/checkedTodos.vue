<template>
  <div class="todo-item">
    <label class="chexkbox">
      <input class="checkbox" type="checkbox" checked @click="this.$emit('thisTodoIsChecked', itemTodo.id)">
      <span class="fake"></span>
    </label>
    <div class="coloumn">
      <h4 class="throught-line">{{ itemTodo.text }}</h4>
      <p  class="throught-line">{{  itemTodo.description }}</p>
      <i class="checked-time">{{ itemTodo.time }}</i>   
    </div>
    <!-- <button class="delete-btn" @click="this.$emit('deleteThisTodo', itemTodo.id)">X</button> -->
  </div>
</template>

<script>
export default {
  name: 'checkedTodos',
  props: [
    'itemTodo',
  ]
}
</script>

<style>
.checked-time {
  background-color: #8E9AA7;
  width: 70px;
  border-radius: 12px;
  padding: 0px 4px;
  color: white;
}
.throught-line {
  text-decoration: line-through;
}
</style>