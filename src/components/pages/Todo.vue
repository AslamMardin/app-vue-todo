<template>
    <div class="row">
        <div class="col-12">
            <h1>Aplikasi Todo Simple</h1>
            <div class="my-3">
                <input type="text" v-model="todo" placeholder="masukan kata" class="form-control" @keyup.enter="addTodo"/>
            </div>
            <hr>
            <List @DoneTodo="doneTodo" @HapusTodo="hapusTodo" :todos="todos" />
            {{ getTotalTodo }}
        </div>
    </div>
</template>

<script>
import List from './List.vue'
export default {
    components: {
        List
    },
    data(){
        return {
            todos : [],
            todo: "",
        }
    },
    mounted(){
        this.todos.push(JSON.parse(localStorage.getItem('todos')))
    },
    computed:{
        getTotalTodo(){
            return "Total List : " + this.todos.length
        }
    }, 
    methods:{
        addTodo(){
            if(this.todo != "") {
                this.todos.push({
                    nama:this.todo,
                    isDone:false,
                    isLoading:false
                });
                this.todo = ''
                this.saveToLocalStorage()
            }else {
                alert('masukan katanya broo')
            }
        },
        hapusTodo(index){
           
                const newTodo = this.todos.filter((todo,i ) => {
                    if(i == index){
                        todo.isLoading = true
                    }
                        return i != index
                })
                setTimeout(() => {
                    this.todos = newTodo
                    this.saveToLocalStorage()
                }, 1000)
           
        },
        doneTodo(index){
            const newTodo = this.todos.filter((todo, i) => {
                if(i == index){
                    todo.isDone = (todo.isDone) ? false : true;
                }
                return todo
            })
            this.saveToLocalStorage()
        },
        saveToLocalStorage(){
            localStorage.setItem('todos', JSON.stringify(this.todos));
        }
    }
}
</script>