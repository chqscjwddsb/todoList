<template>
  <div>
    <ul class="todo-main">
		<transition-group name="todo" appear>
			<my-item v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj"></my-item>
		</transition-group>
        

    </ul>
  </div>
</template>

<script>
import MyItem from './My-item.vue'
export default {
    props:["todos"],
    name:"MyBody",
    components:{
        MyItem
    }
}
</script>

<style scoped>

.todo-enter , .todo-leave-to{
    transform: translatex(100%);
}
.todo-enter-active,.todo-leave-active{
    transition: 0.5s linear;
}
.todo-enter-to,.todo-leave{
    transform:translateX(0);
}
/*main*/
.todo-main {
		margin-left: 0px;
		border: 1px solid #ddd;
		border-radius: 2px;
		padding: 0px;
	}

	.todo-empty {
		height: 40px;
		line-height: 40px;
		border: 1px solid #ddd;
		border-radius: 2px;
		padding-left: 5px;
		margin-top: 10px;
	}
</style>