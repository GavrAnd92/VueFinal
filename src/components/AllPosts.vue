<template>
  <div class="row">

    <div v-if="!newPost" class="row">

    <nav v-show="!select" class="teal">
    <div class="nav-wrapper">
      <form>
        <div class="input-field">
          <input v-model="search" id="search" type="search" required>
          <label class="label-icon" for="search"><i class="material-icons">search</i></label>
          <i class="material-icons" @click="search=''">close</i>
        </div>
      </form>
    </div>
  </nav>

  <ul v-if="!select" class="collapsible">
    <post-tag v-for="(post, index) of searchPost" :key="index" :index="index" :post="post" @remove="remove(index)"
    @selectPost="selectPost(title)" @selectId="selectId(index)"></post-tag>
  </ul>
  
  <select-tag v-else :post="posts[selectIndex]" @back="selectId()" @edit="edit" :addComm="addComm" @deleteComm="deleteComm"></select-tag>

  <div v-if="!select" class="row">
    <div class="col s8"></div>
    <div class="col s4">
      <button @click="newFormToggle()" class="btn waves-effect teal darken-4" type="button" name="action">Додати новий пост
        <i class="material-icons right">add_to_photos</i>
      </button> 
    </div>
  </div>
  
  
  </div>

  <div v-else class="row">
    <div class="col s12 card">
      <new-post-tag :newFormToggle="newFormToggle" :post="newPostData" @addNewPost="add"></new-post-tag>
    </div>
  </div>
  </div>
</template>

<script>
import Post from './Post';
import SelectPost from './selectPost';
import FormPost from './FormPost';
export default {
  data () {
    return {
      posts:[{id: 1, 
              img:'https://cdn.mos.cms.futurecdn.net/ntFmJUZ8tw3ULD3tkBaAtf.jpg', 
              title:'Why Don"t Mountains Grow Forever?', 
              text:'Imagine a world where mountains grow so high, they poke through the upper atmosphere and create a rocky maze for pilots to navigate. Maybe that world exists somewhere in the far reaches of the universe. But on Earth, mountains can"t grow much higher than Mount Everest, which extends 29,029 feet (8,840 meters) above sea level. So what stops our planet"s mountains from growing … forever?',
              comment:[{id:23, text:'hi', time:'16.05.2020, 16:48'}]},
              {id: 2, 
              img:'https://490837.smushcdn.com/1583037/wp-content/uploads/2020/01/MOUNTAIN_header.jpg?lossy=1&strip=1&webp=1', 
              title:'123458?', 
              text:'Imagine a world where mountains grow so high, they poke through the upper atmosphere and create a rocky maze for pilots to navigate. Maybe that world exists somewhere in the far reaches of the universe. But on Earth, mountains can"t grow much higher than Mount Everest, which extends 29,029 feet (8,840 meters) above sea level. So what stops our planet"s mountains from growing … forever?',
              comment:[
                {id:23, text:'hi2', time:'13.05.2020, 10:48'},
                {id:25, text:'hi3', time:'14.05.2020, 16:48'}
              ]}
      ],
      selectIndex: 0,
      select: false,
      newPost: false,
      newPostData: {id: null, img:'', title:'', text:'', comment:[]},
      search:''
    }
  },
  methods:{
    deleteComm(id){
      this.posts[this.selectIndex].comment = this.posts[this.selectIndex].comment.filter(item => item.id !== id)
    },
    newFormToggle(){
      this.newPost = !this.newPost;
    },
    edit({img, title, text}){
      this.posts[this.selectIndex].img = img;
      this.posts[this.selectIndex].title = title;
      this.posts[this.selectIndex].text = text;
      localStorage.setItem('posts', JSON.stringify(this.posts));
    },
    add(obj){
      this.posts.push({id: Date.now().toString(), 
              img:obj.img, 
              title: obj.title, 
              text:obj.text,
              comment:[]});
      this.newFormToggle();
      localStorage.setItem('posts', JSON.stringify(this.posts));
    },
    remove(index){
      this.posts.splice(index, 1);
      localStorage.setItem('posts', JSON.stringify(this.posts));
    },
    local(){
      let posts = localStorage.getItem('posts');
      if(posts){
        posts = JSON.parse(posts);
        this.posts = posts
      } else {
        localStorage.setItem('posts', JSON.stringify(this.posts));
      }
    },
    selectId(index){
      this.selectIndex = index;
      this.select = !this.select;
    },
    addComm(newComment){
      if(newComment != ''){
      this.posts[this.selectIndex].comment.unshift(newComment);
      localStorage.setItem('posts', JSON.stringify(this.posts));
      }
    }
  },
    beforeMount(){
      this.local();

  },
  components:{
    'post-tag' : Post,
    'select-tag': SelectPost,
    'new-post-tag': FormPost
  },
  computed:{
    searchPost(){
      
      return this.posts.filter(post => {
        return post.title.toLowerCase().indexOf(this.search.toLowerCase()) > -1 
      });
      
    }
  }
}
</script>

<style>

</style>
