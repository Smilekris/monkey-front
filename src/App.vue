<template>
  <div class=".app-main">
<el-menu :default-active="activeIndex2" class="el-menu-demo" mode="horizontal" @select="handleSelect" background-color="#545c64" text-color="#fff" active-text-color="#ffd04b">
  <el-menu-item index="1">big中人</el-menu-item>
  <el-submenu index="2">
    <template slot="title">我的工作台</template>
    <el-menu-item index="2-1">选项1</el-menu-item>
    <el-menu-item index="2-2">选项2</el-menu-item>
    <el-menu-item index="2-3">选项3</el-menu-item>
  </el-submenu>
  <el-menu-item index="3"><a href="https://www.ele.me" target="_blank">订单管理</a></el-menu-item>
</el-menu>
<div id="app">
  <p id="headercenter">{{msg}}</p>
  </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      msg: '今晚big什么',
      watchingMsg: 'default msg',
      sum: '',
      activeIndex: '1',
      activeIndex2: '1'
    }
  },
  methods: {
    handleSelect (key, keyPath) {
      console.log(key, keyPath)
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
</style>
