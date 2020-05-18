<template>
  <div class="col s8">
        <div class="card-panel blue lighten-5">
                <div class="chip">
                    <img :src="user.avatar" alt="Contact Person">
                    {{user.name}}
                </div>
                <p>{{comment.text}}</p>
                <div class="row"></div>
                <div class="row">
                  <div class="col s5 m0">
                    <span>{{comment.time}}</span>
                  </div>
                  <div class="col s1 offset-s6">
                    <a href="#!" @click="$emit('deleteComm', comment.id)" class="secondary-content"><i class="material-icons delete">delete_forever</i></a>
                  </div>
                </div>
            </div>
        </div>
</template>

<script>
export default {
    data () {
    return {
      user: JSON.parse(localStorage.getItem('user'))
    }
  },
  props:['comment']
}
</script>

<style>
.m0 span{
  margin-bottom: 0;
  padding-bottom: 0;
  color: #9e9e9e;
}
.card-panel.blue.lighten-5{
  margin-bottom: 0;
  padding-bottom: 0;
}
.material-icons.delete{
  color: red;
}
</style>