<script setup>
import Blog from "./components/Blog.vue"
import {ref} from "vue";
import Pagination from "./components/Pagination.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue"

const blogsData = ref([])

const favourite = ref('')

const postByPage= 10
const firstPost = ref (0)
const lastPost = ref (10)
const loadingSpinner = ref (true)

const next = () =>{
  firstPost.value+= postByPage
  lastPost.value+= postByPage
}

const before = () =>{
  firstPost.value-= postByPage
  lastPost.value-= postByPage
}

const markAsFav = (tittle) =>{
  favourite.value= tittle
}

/*fetch('https://jsonplaceholder.typicode.com/posts').then(response => response.json()).
then(data => blogsData.value=data).
finally(()=>loadingSpinner.value=false) */

const fetchData = async () =>{
try{
const res = await fetch('https://jsonplaceholder.typicode.com/posts')
  blogsData.value = await res.json()
}catch (e) {
 console.log(e)
}finally {
  loadingSpinner.value = false
}
}

fetchData()
</script>


<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-12">
        App
      </div>

      <div class="col-12">
        <h2>My Favourite Post {{favourite}}</h2>
      </div>
      <br>
      <div class="col-2">
        <Pagination @before="before" @next="next" :postbypage="postByPage" :firstPost="firstPost" :lastPost="lastPost" :dataLength="blogsData.length"/>
      </div>
    </div>

    <div class="row" v-if="loadingSpinner">
      <LoadingSpinner />
    </div>
    
    <div class="row" v-else>
      <template  v-for="blog in blogsData.slice(firstPost,lastPost)">
        <Blog v-if="blog.id>0" :title="blog.title" :body="blog.body" :id="blog.id" :key="blog.id" @markAsFav ="markAsFav"/>
      </template>
    </div>
  </div>



</template>