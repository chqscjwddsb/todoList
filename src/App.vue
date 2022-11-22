<template>
  <div id="app">
    <my-header ref="addTodo"></my-header>
    <my-body :todos="todos" :checkTodo= "checkTodo" :delTodo = "delTodo">
    </my-body>
    <my-footer :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"></my-footer>
    

  </div>
</template>

<script>
import MyBody from './components/My-body'
import MyHeader from './components/My-header'
import MyFooter from './components/My-footer'

export default {
  name: 'App',
  data() {
			return {
				//由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
				todos:JSON.parse(localStorage.getItem("todos")) || []
			}
		},
  components: {
    MyHeader,
    MyBody,
    MyFooter,

  },
  methods:{
    addTodo(todoObj){
      // console.log(x)
      this.todos.unshift(todoObj)
    },
    updataTodo(todoObj,e){
      this.todos.forEach((item)=>{
        if(item.id == todoObj.id ) item.title = e.target.value
      })
    },
    checkTodo(id){
      this.todos.forEach((item)=>{
        if(item.id == id) item.done = !item.done
      })
    },
    delTodo(id){
      this.todos = this.todos.filter(item=>item.id !== id)
    },
    checkAllTodo(done){
      this.todos.forEach((item)=>{item.done = done})
    },
    clearAllTodo(){
				this.todos = this.todos.filter((todo)=>{
					return !todo.done
				})
			}

  },
  watch:{
    todos:{
      deep:true,
      handler(value){
        localStorage.setItem("todos",JSON.stringify(value))
      }
    }
  },
  mounted(){
    this.$refs.addTodo.$on("addTodo",this.addTodo)
    this.$bus.$on("delTodo",this.delTodo)
    this.$bus.$on("checkTodo",this.checkTodo)
    this.$bus.$on("updataTodo",this.updataTodo)
  },
  beforeDestroy(){
		this.$bus.$off("[delTodo,checkTodo]")
	}
}
</script>

<style>
#app {
  width: 1000px;
  height: 500px;
  margin: 0 auto;
  border: 1px solid black;
}
</style>
