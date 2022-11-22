<template>
  <div class="todo-header">
    <input type="text"  @keyup.enter="recive" v-model="title"/>
  </div>
</template>

<script>
import {nanoid} from "nanoid"
export default {
    props:["addTodo"],
    name:"MyHeader",
    data(){
        return {
            title:""
        }
    },
    methods:{
        recive(){
            if(!this.title.trim()) return alert("输入的内容不能为空")
            const todoObj = {id:nanoid(),title:this.title,done:false}
            this.$emit("addTodo",todoObj)
            this.title=""
        }
    }

}
</script>

<style scoped>
/*header*/
.todo-header input {
		width: 560px;
		height: 28px;
		font-size: 14px;
		border: 1px solid #ccc;
		border-radius: 4px;
		padding: 4px 7px;
	}

	.todo-header input:focus {
		outline: none;
		border-color: rgba(82, 168, 236, 0.8);
		box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
	}
</style>