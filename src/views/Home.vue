<template>
  <div class="home">
    <el-container>
      <el-header>
        <h2>后台高级管理系统</h2>
        <el-button @click="tui">退出登录</el-button>
      </el-header>
      <el-container>
        <!-- 左侧导航 -->
        <el-aside width="200px">
           <el-menu
      default-active="2"
      class="el-menu-vertical-demo"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b"
      router
    >
      <!-- 用户管理 -->
      <el-submenu index="user">
        <template slot="title">
          <i class="el-icon-user-solid"></i>
          <span>用户管理</span>
        </template>
        <el-menu-item index="about">用户列表</el-menu-item>
      </el-submenu>
      <!-- 权限管理 -->
      <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-s-marketing"></i>
          <span>权限管理</span>
        </template>
       
      </el-submenu>
      <!-- 商品管理 -->
      <el-submenu index="2">
        <template slot="title">
          <i class="el-icon-s-cooperation"></i>
          <span>商品管理</span>
        </template>

      </el-submenu>
      <!-- 订单管理 -->
      <el-submenu index="3">
        <template slot="title">
          <i class="el-icon-s-order"></i>
          <span>订单管理</span>
        </template>
   
      </el-submenu>
      <!-- 数据统计 -->
      <el-submenu index="4">
        <template slot="title">
          <i class="el-icon-s-order"></i>
          <span>数据统计</span>
        </template>

      </el-submenu>
    </el-menu>

        </el-aside>
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
  name: "Home",
  components: {},
  data() {
    return {};
  },
  methods:{
    // 退出
     tui() {
      localStorage.removeItem("TOKEN");
      window.location.reload();
    },
  }
};
</script>


<style scoped>
@import "../assets/style.css";
.el-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #fff;

}
</style>
