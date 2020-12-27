<template>
  <div>
    <form @submit="addTodo">
      <input type="text" v-model="title" name="title" placeholder="Add Todo.." class="box" />
      <input type="submit" value="ADD" class="btnAdd" />
      <input type="button" value="CLEAR ALL" class="btnclear" @click="$emit('clear-all')" />
    </form>
  </div>
</template>
<script>
import Vue from "vue";
import UUID from "vue-uuid";
Vue.use(UUID);
export default {
  name: "Addtodo",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();

      const newTodo = {
        id: this.$uuid.v4(),
        title: this.title,
        completed: false,
      };
      if (this.title !== "") {
        this.$emit("add-todo", newTodo);
        this.title = "";
      }
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  color:  rgb(245, 245, 245);
  flex: 10;
  padding: 5px;
}
input[type="submit"] {
  flex: 2;
  background: #0f6e94;
  padding: 15px 3px;
}
input[type="button"]{
  flex: 2;
  background: #d46c77;
  padding: 15px 3px;
}
::placeholder {
  color: whitesmoke;
}
.btnclear {
  display: inline-block;
  padding: 11px 21px;
  font-size: 18px;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
  outline: none;
  color: #fff;
  background-color: #d46c77;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
}
.btnclear:hover {
  background-color: #3e8e41;
}
.btnclear:active {
  background-color: #d46c77;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}
.btnAdd {
  display: inline-block;
  padding: 1px 2px;
  font-size: 15px;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
  outline: none;
  color: #fff;
  background-color: #4CAF50;
  border: none;
  border-radius: 15px;
  box-shadow: 0 9px #999;
}
.btnAdd:hover {
  background-color: #3e8e41;
}
.btnAdd:active {
  background-color: #0f6e94;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
}
.box{
   background-color: #5e6364;
   border-color: #fff;
  border-radius: 15px;
  font-size: 16px;
  color: yellow;
  text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;
  transform: scaleY(1.152);
}
</style>