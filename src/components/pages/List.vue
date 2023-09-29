<template>
   <ol class="list-group list-group-numbered">
  <li class="list-group-item d-flex justify-content-between align-items-start" v-for="(todo, i) in todos" :key="todo">
    <div class="ms-2 me-auto">
      <div class="fw-bold">
        <del v-if="todo.isDone" :class="{'text-danger':todo.isDone}">{{ todo.nama }}</del>
        <span v-else>{{ todo.nama }}</span>
        </div>
    </div>
    <span style="cursor: pointer;" @click="hapusTodo(i)" class="badge bg-danger rounded-pill">
        <span v-if="todo.isLoading">...</span>
        <i class="bi bi-trash3-fill" v-else></i>
    </span>
    <span style="cursor: pointer;" @click="doneTodo(i)" class="badge bg-success ml-1 rounded-pill" :class="{'bg-info':todo.isDone}">
        <i class="bi bi-x" v-if="todo.isDone"></i>
        <i class="bi bi-check2-circle" v-else></i>
    </span>
    
  </li>
  
</ol>
</template> x

<script>
    export default {
        props: ["todos"],
        emits:['HapusTodo', 'DoneTodo'],
        methods:{
            hapusTodo(index){
                this.$emit('HapusTodo', index)
            },
            doneTodo(index) {
                this.$emit('DoneTodo', index)
            }
        },
        
    }
</script>