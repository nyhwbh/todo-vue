<template>
  <div>
    <transition-group name="modal-fade" tag="ul">
        <li v-for="(todoItem, index) in this.storedTodoItems" v-bind:key="todoItem.item" class="shadow" >
          <span v-on:click="toggleComplete({todoItem,index})">
            <i class="checkBtn fa-solid fa-check"
            v-bind:class="{checkBtnCompleted: todoItem.completed}"></i>
          </span>
          <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
          <span class="removeBtn" v-on:click="removeTodo({todoItem,index})">
            <i class="fa-solid fa-trash-can"></i>
          </span>
        </li>
    </transition-group>
  </div>
</template>

<script>
import { mapGetters,mapMutations } from 'vuex'

export default {
  methods :{
    ...mapMutations({
      removeTodo: 'removeOneItem', //인자는 자동으로 넘겨주고 있다
      toggleComplete: 'toggleOneItem'
  })
  },
  computed: {
    // todoItems() {
    //   return this.$store.getters.storedTodoItems
    // }
    ...mapGetters(['storedTodoItems'])
    // ...mapGetters({
    //   todoItems:storedTodoItems
    // })
  }
  
}
</script>

<style scoped>
ul{
  list-style-type: none;
  padding-left: 8px;
  margin-top: 0;
  text-align: left;
}

li{
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin:0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left:auto;
  color:#de4343
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right:5px;
  margin-top: 18px;
}
.checkBtnCompleted {
  color: #b3adad
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: all 1s ease;
}
.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>