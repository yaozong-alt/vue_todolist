<template>
   <li :class="{completed:todo.hasCompleted,editing:editedTodo === todo}">
       <div class="view">
        <input type="checkbox" name="" id="toggle" class="toggle" v-model="todo.hasCompleted">
        <label @dblclick="editTodo(todo)">{{todo.value}}</label>
        <button class="destroy" @click=" deletedTodo(todo.id)"></button>
       </div>
       <input type="text" class="edit" 
       v-focus 
       v-model="editedTodo.value" 
       @keyup.enter="doneTodo"
       @blur="doneTodo"
       @keyup.esc="canncelTodo(index)"

       >
   </li>
</template>

<script>
    export default {
        name:"Item",
        props:['todo','index'],
        data(){
            return {
                editedTodo:"",
                value:"",//存储当前的todo的value

            }
        },
        methods:{
            deletedTodo(id){
                this.$parent.todoDatas = this.$parent.todoDatas.filter((value) => {
                    return !(value.id == id);
                    //相等的就会被过滤掉
                })
            },
            editTodo(todo){
                this.value = todo.value;
                this.editedTodo = todo;
            },
            doneTodo(){
                this.editedTodo = ''
            },
            canncelTodo(index){
                this.$parent.todoDatas[index].value = this.value;
                this.editedTodo = ''

            }
        },
        directives:{
            focus(el){
                el.focus();
            }
        }

    }
</script>

<style scoped>

</style>