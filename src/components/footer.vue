<template>
    <footer class="footer">
        <span class="todo-count">
            <strong>{{todoNum}}</strong>
            <span v-if="todoNum <= 1"> item left</span>
            <span v-else> items left</span>
        </span>
        <ul class="filters">
            <li><a href="#/all" @click=" viewTodo('all')">All</a></li>
            <li><a href="#/active" @click=" viewTodo('active')">Active</a></li>
            <li><a href="#/completed" @click=" viewTodo('completed')">Completed</a></li>
        </ul>
        <button class="clear-completed" @click="clearCompelted">Clear Completed</button>
    </footer>
</template>

<script>
    export default {
        name:'Footer',
        computed:{
            todoNum(){
                return this.$parent.todoDatas.filter(value => {
                    return !value.hasCompleted;
                }).length
            }
        },
        methods:{
           viewTodo(flag){
               console.log('flag被调用了')
                this.$parent.view = flag;
            },
            clearCompelted(){
                 this.$parent.todoDatas = this.$parent.todoDatas.filter((value) => {
                    return !value.hasCompleted
                })
            }
        }

    }
</script>

<style scoped>

</style>