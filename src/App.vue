<template>
  <div id="app" class="container">
   <header-tag></header-tag>
   <posts-tag></posts-tag>
  </div>
</template>

<script>
import Header from './components/Header';
import Posts from './components/AllPosts'
export default {
  name: 'app',
  data () {
    return {
      
    }
  },
  components:{
    'header-tag': Header,
    'posts-tag': Posts
  }
}
</script>

<style>

</style>
