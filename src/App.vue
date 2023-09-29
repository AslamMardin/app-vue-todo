<script>
import Home from './components/pages/Home.vue'
import About from './components/pages/About.vue'
import Post from './components/pages/Post.vue'
import Todo from './components/pages/Todo.vue'
export default {
  data(){
    return {
      tabs:['Home', 'Post', 'About', 'Todo'],
      currentTab:'Home'
    }
  },
  computed:{
    currentTabComponent(){
      return this.currentTab.toLocaleLowerCase();
    }
  },
  components:{
    Home, About, Post, Todo
  }
}
</script>

<style>
  .active {
    color:red !important
  }
</style>

<template>
  <!-- navbar -->
 
 <nav class="navbar navbar-expand-lg bg-body-tertiary">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Belajar Vue</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item" v-for="tab in tabs" :key="tab">
          <a class="nav-link" :class="{active:currentTab==tab}" @click.prevent="currentTab = tab" aria-current="page" href="#">{{ tab }}</a>
        </li>
    
      </ul>
     
    </div>
  </div>
</nav>
<!-- end navbar -->

<div class="container mt-5">
  <div class="row">
    <div class="col-8">
      <!-- main -->
      <KeepAlive>
        <component :is="currentTabComponent" />
      </KeepAlive>
      <!-- end main -->
    </div>
  </div>
</div>
</template>
