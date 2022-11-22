<template>
  <div class="todo-footer" v-show="total">
    <label>
		<!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
		<input type="checkbox" v-model = "isAll"/>
	</label>
	<span>
		<span>已完成{{done}}</span> / 全部{{total}}
	</span>
	<button btn-danger @click ="clearAllTodo">清除已完成任务</button>
  </div>
</template>

<script>




export default  {
    props:["todos","checkAllTodo","clearAllTodo"],
    name:"MyFooter",
    computed:{
        total(){
            return this.todos.length
        },
        done(){
            return this.todos.reduce((pre,todo)=>pre + (todo.done? 1:0),0)
        },
        isAll:{
            get(){
                return this.done === this.total && this.total>0
            },
            set(value){
                this.checkAllTodo(value)
            }
        }
    },
   

}
</script>

<style scoped>
/*footer*/
.todo-footer {
		height: 40px;
		line-height: 40px;
		padding-left: 6px;
		margin-top: 5px;
	}

	.todo-footer label {
		display: inline-block;
		margin-right: 20px;
		cursor: pointer;
	}

	.todo-footer label input {
		position: relative;
		top: -1px;
		vertical-align: middle;
		margin-right: 5px;
	}

	.todo-footer button {
		float: right;
		margin-top: 5px;
	}
</style>