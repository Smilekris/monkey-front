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
  <!-- <el-menu-item index="3"><a href="https://www.ele.me" target="_blank">订单管理</a></el-menu-item> -->
</el-menu>
<div id="app">
  <div style="text-align:right; margin: 5px">{{surfing}},{{paperViews}}</div>
  <p id="headercenter">{{msg}}{{menu}}</p>
  </div>
   <el-button type="primary" @click="getRandomMenus" style="display:block;margin:0 auto" :disabled="pickUpBol">抽奖</el-button>
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
      timer: '',
      pickUpBol: false,
      surfing: '',
      paperViews: ''
    }
  },
  created () {
    this.getSurfing()
    this.getPaperViews()
    // this.getRandomMenus()
    // this.menu = setInterval(this.menus.get(), 1000)
  },
  mounted () {
  },
  methods: {
    handleSelect (key, keyPath) {
      console.log(key, keyPath)
    },
    getSurfing () {
      var url = 'http://kris0806.cn/monkey/statistics/surf'
      axios.get(url).then(res => {
        this.surfing = res.data.result
      })
    },
    getPaperViews () {
      var url = 'http://kris0806.cn/monkey/statistics/sum'
      axios.get(url).then(res => {
        this.paperViews = res.data.result
      })
    },
    getRandomMenus () {
      var url = 'http://kris0806.cn/monkey/statistics/random-menus'
      if (this.pickUpBol === true) {
        return
      }
      axios.get(url).then(res => {
        this.pickUpBol = true
        this.menus = res.data.result
        this.timer = setInterval(this.setMenuName, 200)
      })
    },
    setMenuName () {
      this.menu = this.menus[this.count].menuName
      this.count += 1
      if (this.count === this.menus.length) {
        this.count = 0
        this.pickUpBol = false
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
