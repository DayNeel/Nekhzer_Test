<template>

  <div id="app">
  
    <div class="album">
      <div class="container">
        <h5 class="title">Пользователи GitHub</h5>
        <div class="row">
          <div class="card" style="width: 18rem;" v-bind:key="user.id" v-for="user in users">
            <img class="card-img-top" :src='user.avatar_url' alt="Card image cap">
            <div class="card-body">
              <h5 class="card-title">{{user.login}}</h5>
              <p class="card-text">Тип: {{user.type}}</p>
              <a :href="user.html_url" target="_blank" class="btn btn-primary">Профиль</a>
            </div>
          </div>
        </div>
        <div class="bt" v-if='!loader'>
          <button class="bt1 btn-primary" v-if='page>1' v-on:click="pre">Назад</button>
          <button class="bt1 btn-primary" v-on:click="next">Вперед</button>
        </div>
      </div>
        <br>
        
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data: function() {
    return { 
      users:{},
      page:100,
      perpage:9,
      loader:false
    }
  },
  methods:{
    getusers:function(){
      var url='https://api.github.com/users?since='+this.page+'&per_page='+this.perpage
      var self=this
      console.log(url)
      this.loader=true
      axios
      .get(url)
      .then(response => {
        self.users=response.data
        console.log(response.data)
        self.loader=false})
        .catch(error => console.log(error));
    },
    next:function()
    {
      this.page=this.page+this.perpage
      this.getusers()
    },
    pre:function()
    {
      this.page=this.page-this.perpage
      this.getusers()
    },
  },
  mounted() 
  {
    this.getusers()
  }
}
</script>

<style>
.user{
  width: 30%;
}

img{
  max-width: 18rem;
}

.bt{
    font-size: 15px;
    color: #fff;
    line-height: 1.2;
    text-transform: uppercase;
    display: -webkit-box;
    display: -webkit-flex;
    display: -moz-box;
    display: -ms-flexbox;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 20px;
    font-size: 15px;
    color: #fff;
    line-height: 1.2;
    text-transform: uppercase;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 20px;
    margin-top: 2%;
}

.bt1{
   display: inline-block;
    font-weight: 400;
    color: #212529;
    text-align: center;
    vertical-align: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    background-color: transparent;
    border: 1px solid transparent;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: 0.25rem;
    width: 100px;
}

.btn{
    font-size: 15px;
    color: #fff;
    line-height: 1.2;
    text-transform: uppercase;
    display: -webkit-box;
    display: -webkit-flex;
    display: -moz-box;
    display: -ms-flexbox;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 20px;
}

.title{
    display: block;
    font-size: 35px;
    color: #333333;
    line-height: 1.2;
    text-align: center;
}

.app{
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  overflow: auto;
  display: flex;
}

.container {
    width: 390px;
    background: #fff;
    border-radius: 10px;
    overflow: hidden;
    padding: 77px 55px 33px 55px;
    box-shadow: 0 5px 10px 0px rgba(0, 0, 0, 0.1);
    -moz-box-shadow: 0 5px 10px 0px rgba(0, 0, 0, 0.1);
    -webkit-box-shadow: 0 5px 10px 0px rgba(0, 0, 0, 0.1);
    -o-box-shadow: 0 5px 10px 0px rgba(0, 0, 0, 0.1);
    -ms-box-shadow: 0 5px 10px 0px rgba(0, 0, 0, 0.1);
}

.album{
    width: 100%;
    min-height: 100vh;
    display: -webkit-box;
    display: -webkit-flex;
    display: -moz-box;
    display: -ms-flexbox;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    padding: 15px;
    background: #f2f2f2;
}

.row{
  display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding-top: 13px;
}

.body{
  font-family: fantasy;
}
</style>
