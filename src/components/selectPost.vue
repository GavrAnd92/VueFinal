<template>
<div>
      <div v-if="edit" class="row card">
        <div class="col s4">
          <div class="row"></div>
          <img :src="post.img" width="215">
        </div>
        <div class="col s8">
          <div class="row">
            <div class="col s9">
              <h5>{{post.title}}</h5>
            </div>
            <div class="col s2">
              <div class="row"></div>
              <a class="waves-effect teal lighten-2 btn-small" @click="changePost()">Редагувати</a>
              <div class="row"></div>
              <a class="waves-effect red darken-4 btn-small" @click="$emit('back')">Повернутися</a>
            </div>
          </div>
          <div class="row">
            <div class="col s12">
              <p>{{post.text}}</p>
            </div>
            <div class="row"></div>
            <div class="row">
              <div class="col s9">
                <div class="row">
                    <div class="col s12">
                    <div class="row">
                        <div class="input-field col s12">
                        <i class="material-icons prefix">textsms</i>
                        <input v-model="newComm" type="text" id="autocomplete-input" class="autocomplete">
                        <label for="autocomplete-input">Залиште коментар</label>
                        </div>
                    </div>
                    </div>
                </div>
              </div>
              <div class="col s2">
                  <div class="row"></div>
                        <a @click="selectAddComm(),newComm=''" class="waves-effect teal lighten-2 btn-small"><i class="material-icons right">send</i></a>
                    </div>
                </div>
            <div class="row">
              <comm-tag v-for="(comm, index) in post.comment" :key="index" :comment="comm" 
              @deleteComm="deleteComm"></comm-tag>
            </div>
          </div>
        </div>
      </div>
      <div v-else class="row card">
          <form-tag :fromSelectPost="true" :post="post" :changePost="changePost" @edit="editPost"></form-tag>
      </div>
  </div>
    
</template>

<script>
import FormPost from './FormPost';
import CommentPost from './Comment';
export default {
  data () {
    return {
      edit: true,
      formPost : {},
      user: JSON.parse(localStorage.getItem('user')),
      newComm:''
    }
  },
  methods:{
    deleteComm(id){
      this.$emit('deleteComm', id);
    },
    editPost(editObjPost){
        this.$emit('edit', editObjPost);
    },
   changePost(){
       this.edit = !this.edit;
   },
   selectAddComm(){
     let date = new Date;
     let time = date.toLocaleString("ru", {
      hour: 'numeric',
      minute: 'numeric',
      day: 'numeric',
      month: 'numeric',
      year: 'numeric'
     });
     let obj = {
       id: Date.now().toString(),
       text: this.newComm,
       time: time
     }
     this.addComm(obj);
   }
  },
    beforeMount(){
     
  },
  props:['post','addComm'],
  components:{
    'form-tag': FormPost,
    'comm-tag':CommentPost
  }
}
</script>

<style>
.post{
  margin: 0;
}

</style>
