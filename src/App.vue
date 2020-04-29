<template>
 <section class="todoapp">
   <header class="header">
     <h1>Todos</h1>
     <input type="text" placeholder="what need to do!" 
     class="new-todo" 
     id="new-todo" 
     v-model="newTodo"
     @keyup.enter="addTodo"
      >
   </header>
   <section class="main">
     <input type="checkbox" class="toggle-all" id="toggle-all" v-model='isAll'>
     <label for="toggle-all"></label>
   </section>
   <ul class="todo-list">
     <Item v-for="(value,index) in  filterTodo" :key="index" :todo="value" :index="index"/>
   </ul>
   <Footer/>
 </section>
 
</template>

<script>
import Item from './components/item';
import Footer from './components/footer';
  export default {
    name:'App',
    components:{
      Item,Footer,
    },
    data(){
      return {
        todoDatas:[],//用来存放todo;
        newTodo:"",//用来存放todo的value;
        view:'all',//默认是all;
      }
    },
    methods:{
      addTodo(){
        if(this.newTodo === '') return ;
        let todo = {};
        todo.id = new Date().getTime();
        todo.value = this.newTodo;
        todo.hasCompleted = false;
        this.todoDatas.push(todo);
        this.newTodo = '';
      },
    },
    computed:{
      isAll:{
        get(){
          if(this.todoDatas.length === 0) return;
          return this.todoDatas.length === this.todoDatas.filter(value => {
            return value.hasCompleted;
          }).length;
        },
        set(value){
            this.todoDatas.map((todo) => {
              todo.hasCompleted = value;
              return todo;
            })
        }
      },
      filterTodo(){
        switch(this.view){
          case 'all':
            return this.todoDatas;
          case 'active':
            return this.todoDatas.filter(value => {
              return !value.hasCompleted;
            });
          case 'completed':
            return this.todoDatas.filter(value => {
              return value.hasCompleted;
            })
          default :
            return this.todoDatas;
        }
      }
    },


  }
</script>

<style scoped>

</style>