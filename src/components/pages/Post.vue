<template>
    <h3>ini halaman post</h3>
    <ul class="list-group">
  <li class="list-group-item" v-for="post in posts" :key="post">{{ post }}</li>
 
</ul>
</template>

<script>
export default {
    data(){
        return {
            posts:[]
        }
    },
    async created(){
        const data = await fetch('https://swapi.dev/api/planets/')
        const {results} = await data.json();
        results.forEach(planet => this.posts.push(planet.name))
    }
}
</script>