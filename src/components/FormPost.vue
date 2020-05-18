<template>
  <div class="row">
    <div class="col s12">
      <ul>
        <li>
          <div class="row">
            <div class="col s10 offset-s1">
            <label for="name">Введіть назву</label>
              <input v-model="title" id="name" type="text" class="validate">
            </div>
          </div>
          <div class="row">
            <div class="col s10 offset-s1">
              <label for="url">Вставте URL зображення</label>
              <input v-model="img" id="url" type="text" class="validate">
            </div>
            <div class="col s10 offset-s1">
                <label for="">Опис</label>
                <textarea v-model="textPost" data-length="500"></textarea>
            </div>
          </div>
          <div class="row">
            <a @click="changePostForm()" class="waves-effect waves-light btn-small col s2 offset-s1">Зберегти</a>
            <a @click="notSave()" class="waves-effect waves-light btn-small col s2 offset-s1  red darken-4">Відміна</a>
          </div>
        </li>
        
    </ul>
  </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      img:this.post.img,
      title:this.post.title,
      textPost:this.post.text
    }
  },
  methods:{
    notSave(){
      if(this.changePost){
        this.changePost()
      } else {
        this.newFormToggle()
      }
    },
    changePostForm(){
        if(this.img != '' && this.title != '' && this.textPost != '' && this.fromSelectPost){
            this.changePost();
            this.$emit('edit', {img:this.img, title:this.title,text:this.textPost});
        }
        if(this.newFormToggle){
          if(this.img != '' && this.title != '' && this.textPost != ''){
            this.$emit('addNewPost', {img:this.img, title:this.title,text:this.textPost});
          }
        }
    }
  },
  props:['post','fromSelectPost', 'changePost', 'newFormToggle'],
    beforeMount(){
     
    }
   
}
</script>

<style>
textarea{
    height: 120px;
    border:none;
    border-bottom: 1px solid grey;
}
textarea:focus{
    border:none;
    outline:none;
    border-bottom: 2px solid teal;
}
</style>
