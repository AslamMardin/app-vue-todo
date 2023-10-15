<template>
    <div class="row">
        <div class="col-12">
            <h3>Daftar Tugas UHM XVII</h3>
            <div class="my-3">
                <input type="text" v-model="todo" placeholder="masukan kata" class="form-control" @keyup.enter="addTodo"/>
            </div>
            <hr>
            <List @doneTodo="doneTodo" @hapusTodo="hapusTodo" :todos="list" />
            {{ getTotalTodo }}
            <p>
                <i>Product By <b>Aslam Mardin, S.Kom</b></i>
            </p>
        </div>
    </div>
</template>

<script>
import { computed, onMounted, reactive, ref, toRefs, onBeforeMount } from 'vue';
import List from './List.vue'
export default {
    components: {
        List
    },
    setup() {
        const todo = ref("");
        const todos = reactive({
            list:[]
        });

        const addTodo = ()  => {
            console.log('sas')
            if(todo.value != "") {
                todos.list.push({
                    nama:todo.value,
                    isDone:false,
                    isLoading:false
                })
                todo.value = ''
                console.log(todos.list)
                saveToLocalStorage()
            }else {
                alert('masukan katanya broo')
            }

        }

        const hapusTodo = (index) => {
            const newTodo = todos.list.filter((todo,i ) => {
                    if(i == index){
                        todo.isLoading = true
                    }
                        return i != index
                })
                setTimeout(() => {
                    todos.list = newTodo
                    saveToLocalStorage()
                }, 1000)
        }

        const doneTodo = (index) => {
            const newTodo = todos.list.filter((todo, i) => {
                if(i == index){
                    todo.isDone = (todo.isDone) ? false : true;
                }
                return todo
            })
            saveToLocalStorage()
        }

        const saveToLocalStorage = () => {
            localStorage.setItem('todos', JSON.stringify(todos.list));
        }

        onMounted(() => {
            // if(todo.list == null) {
            //     todos.list = []
            // }else {
            //     todos.list = JSON.parse(localStorage.getItem('todos'));
            // }

            const items = localStorage.getItem('todos');
            todos.list = items ? JSON.parse(items) : []
        })
       
        const getTotalTodo = computed(() => {
                return "Total Agenda : " + todos.list.length
        })
        return {
            todo,
            ...toRefs(todos),
            getTotalTodo,
            addTodo,
            hapusTodo,
            doneTodo,
            saveToLocalStorage
        }
    },
    
 
}
</script>
