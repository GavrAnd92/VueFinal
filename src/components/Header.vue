<template>
  <div class="row">
    <div class="col s12">
      <ul class="collection">
        <li v-if="isChange">
          <div class="row">
            <div class="input-field col s10 offset-s1">
              <input @change="dangerName = ''" v-model="name" id="name" type="text" class="validate">
              <label :class="dangerName" for="name">Введіть ім'я</label>
            </div>
          </div>
          <div class="row">
            <div class="input-field col s10 offset-s1">
              <input @change="dangerUrl = ''" v-model="avatar" id="url" type="text" class="validate">
              <label :class="dangerUrl" for="url">Вставте URL зображення</label>
            </div>
          </div>
          <div class="row">
            <a @click="save()" class="waves-effect waves-light btn-small col s2 offset-s1">Зберегти</a>
            <a @click="notSave()" class="waves-effect waves-light btn-small col s2 offset-s1  red darken-4">Відміна</a>
          </div>
        </li>
        <li v-else class="collection-item avatar">
          <img :src="user.avatar" alt="" class="circle">
          <span class="title">{{user.name}}</span>
          <p><a href="#" @click="isChange = true">Редагувати</a><br>
          </p>
        </li>
        
    </ul>
  </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      user:{
        avatar:'https://vokrug.tv/pic/person/2/b/f/4/2bf448098b7badf3b37e87c510da29bc.jpeg',
        name:'Андрій'
      },
      avatar: '',
      name:'',
      isChange: false,
      dangerName:'',
      dangerUrl:''
    }
  },
  methods:{
    notSave(){
      this.isChange = false;
      this.avatar = '';
      this.name = '';
      this.dangerName = '';
      this.dangerUrl = '';
    },
    save(){
      if(this.avatar != '' && this.name != ''){
        this.isChange = false;
        this.user.avatar = this.avatar;
        this.user.name = this.name;
        this.avatar = '';
        this.name = '';
        this.dangerName = '';
        this.dangerUrl = '';
        localStorage.setItem('user', JSON.stringify(this.user));

      } else if(this.avatar == ''){
        this.dangerUrl = 'red-text';
        if( this.name == ''){
          this.dangerName = 'red-text';
        }
      } else {
        this.dangerName = 'red-text';
      }
    }
  },
    beforeMount(){
      let user = localStorage.getItem('user');
      if(user){
        user = JSON.parse(user);
        this.user = user
      } else {
        localStorage.setItem('user', JSON.stringify(this.user));
      }
  }
}
</script>

<style>

</style>
