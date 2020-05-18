<template>
<div>
    <li>
      <div class="collapsible-header">
        <div class="col s12 post">
          <div class="col s3">
            <img :src="post.img" alt="" width="150">
          </div>
          <div class="col s7 card-title">
            <h6>{{post.title}}</h6>
            <p>{{post.text.slice(0, 35)+'...'}}</p>
          </div>
          <div class="col s2">
            <a class="waves-effect red darken-1 btn-small" @click.stop="remove">Видалити</a>
            <div class="row"></div>
            <a class="waves-effect teal lighten-2 btn-small" @click="selectPost()">Переглянути</a>
          </div>
        </div>
      </div>
    </li>
   
  </div>
    
</template>

<script>
export default {
  data () {
    return {
      
    }
  },
  methods:{
    remove(){
      this.$emit('remove', this.index);
    },
    selectPost(){
      this.$emit('selectId', this.index);
    }
  },
    beforeMount(){
        
  },
  props:['post', 'index']
}
</script>

<style>
.post{
  margin: 0;
}

</style>
