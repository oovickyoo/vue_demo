<template>

  <div id="app">
    <h1>{{title}}</h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isfinish}" v-on:click="toggleFinish(item)">
        {{item.lable}}
      </li>
    </ul>
    <!-- <img src="./assets/logo.png"> -->
    <!-- <router-view></router-view> -->
  </div>
</template>

<script>
import Store from './store'
console.log(Store)
export default {
  name: 'app',
  data: function(){
    return {
      title: 'this is a todo list',
      items: Store.fetch(),
      newItem:''
    }
  },
  watch:{
    items:{
      handler:function(items){
        Store.save(items)

      },
      deep:true
    }
  },
  methods:{
    toggleFinish:function (item) {
      item.isfinish=true
      console.log(item)// body...
    },
    addNew:function(){
      this.items.push({
        lable:this.newItem,
        isfinish:false
      })
      console.log(this.newItem)
      this.newItem=''
      Store.save
    }
  }
}
</script>

<style>
.finished {
  text-decoration: line-through;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
