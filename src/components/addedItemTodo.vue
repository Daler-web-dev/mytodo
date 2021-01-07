<template>
  <div class="todo-item">
    <label class="chexkbox">
      <input class="checkbox" type="checkbox" @click="this.$emit('thisTodoIsChecked', itemTodo.id)">
      <span class="fake"></span>
    </label>
    <div class="coloumn" v-bind:title="message" @click="this.$emit('changetodo', itemTodo.id)">
      <h4>{{ itemTodo.text }}</h4>
      <p>{{  itemTodo.description }}</p>
      <i class="time">{{ itemTodo.time }}</i> 
    </div>
    <!-- <button class="delete-btn" @click="this.$emit('deleteThisTodo', itemTodo.id)">X</button> -->
  </div>
</template>

<script>
export default {
  name: 'itemOftodods',
  props: [
    'itemTodo',
  ],
  data() {
    return {
      message: 'Нажмите чтобы изменить',
    }
  }
}
</script>

<style>

.checkbox {
  display: none;
}
.fake {
  display: inline-block;
  width: 21px;
  height: 21px;
  border: 1px solid black;
  position: relative;
  border-radius: 100%;
}
.fake::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: block;
  width:  21px;
  height: 21px;
  background-color: #004DFF;
  border-radius: 100%;
  border: none;
  opacity: 0;
  transition: .2s;
}
.checkbox:checked + .fake::before {
  opacity: 1;
  border: none;
}

</style>