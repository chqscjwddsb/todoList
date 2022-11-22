<template>
  <div>
    
      <li>
        <label>
          <input type="checkbox" :checked="todo.done" @change="handleTodo(todo.id)" />
          <span v-show="!todo.isEdit">{{todo.title}}</span>
          <input
            type="text"
            :value="todo.title"
            v-show="todo.isEdit"
            @blur="blurItem(todo,$event)"
            @keyup.enter="EnterInput(todo,$event)"
            ref="inputTitle"
          />
        </label>
        <button @click="DeleteItem(todo.id)">删除</button>
        <button @click="EditItem(todo)">编辑</button>
      </li>
    
  </div>
</template>

<script>
export default {
  props: ["todo"],
  name: "MyItem",
  methods: {
    handleTodo(id) {
      this.$bus.$emit("checkTodo", id);
    },
    DeleteItem(id) {
      this.$bus.$emit("delTodo", id);
    },
    EditItem(todo) {
      if (todo.hasOwnProperty.call("isEdit")) {
        todo.isEdit = true;
      } else {
        this.$set(todo, "isEdit", true);
      }
      this.$nextTick(function() {
        this.$refs.inputTitle.focus();
      });
      // setTimeout(() => {
      // 	this.$refs.inputTitle.focus()
      // }, 3000);
    },
    blurItem(todo, e) {
      this.$bus.$emit("updataTodo", todo, e);
      todo.isEdit = false;
    },
    EnterInput(todo, e) {
      this.$bus.$emit("updataTodo", todo, e);
      todo.isEdit = false;
    }
  }
};
</script>

<style scoped>

li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background-color: #ddd;
}

li:hover button {
  display: block;
}
</style>