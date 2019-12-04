<template>
  <div class="app-main">
<el-menu :default-active="activeIndex2" class="el-menu-demo" mode="horizontal" @select="handleSelect" background-color="#545c64" text-color="#fff" active-text-color="#ffd04b">
  <el-menu-item index="1">big中人</el-menu-item>
  <el-submenu index="2">
    <template slot="title">big圈</template>
    <el-menu-item index="2-1">big圈动态</el-menu-item>
    <el-menu-item index="2-2">big素材</el-menu-item>
    <el-menu-item index="2-3">big论坛</el-menu-item>
  </el-submenu>
  <el-menu-item index="3"><a href="https://www.ele.me" target="_blank">订单管理</a></el-menu-item>
</el-menu>
<div id="app">
  <p id="headercenter">{{msg}}{{menu}}</p>
  </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  data () {
    return {
      msg: '今晚big',
      watchingMsg: 'default msg',
      sum: '',
      activeIndex: '1',
      activeIndex2: '1',
      menus: [],
      menu: '什么',
      count: 0,
      timer: ''
    }
  },
  created () {
    this.getRandomMenus()
    // this.menu = setInterval(this.menus.get(), 1000)
  },
  mounted () {
  },
  methods: {
    handleSelect (key, keyPath) {
      console.log(key, keyPath)
    },
    getRandomMenus () {
      var url = 'http://kris0806.cn/monkey/statistics/random-menus'
      axios.get(url).then(res => {
        this.menus = res.data.result
        console.log('a' + this.menus[0].menuName)
        this.timer = setInterval(this.setMenuName, 200)
      })
    },
    setMenuName () {
      debugger
      this.menu = this.menus[this.count].menuName
      this.count += 1
      if (this.count === this.menus.length) {
        clearInterval(this.timer)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
#headercenter {
  margin: 50px;
  font: "PingFang SC";
  font-size: 25px;
}
  .app-main {
    width: 100%;
    height: 100%;
  }
  *{
margin:0;
padding:0
}
  html,body{
width:100%;
height:100%
}
</style>
