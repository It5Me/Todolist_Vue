<template>
    <div>
       <div v-bind:key="todo.id" v-for="todo in sortarray">
          <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo',todo.id)"/>
       </div>

    </div>
</template>
<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "Todos",
  components:{
    TodoItem
  },
  props: ["todos"],
  computed:{
    sortarray:function(){
      return this._.orderBy(this.todos,["completed",false])
    }
  }
};
</script>
<style scoped>

</style>

 