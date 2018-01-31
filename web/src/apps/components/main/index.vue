<template>
  <el-container>
    <el-header>
      <nav>
        <el-menu :default-active="activeIndex" class="el-menu-custom" mode="horizontal" @select="handleSelect" 
        background-color="#545c64"
        text-color="#fff"
        active-text-color="#ffd04b">
          <el-menu-item index="1">Logo</el-menu-item>
          <!-- <el-submenu index="2">
            <template slot="title">我的工作台</template>
            <el-menu-item index="2-1">选项1</el-menu-item>
            <el-menu-item index="2-2">选项2</el-menu-item>
            <el-menu-item index="2-3">选项3</el-menu-item>
          </el-submenu> -->
          <el-menu-item index="3"><a @click="exit">退出</a></el-menu-item>
        </el-menu>
      </nav>
    </el-header>
    <el-main>
      <router-view></router-view>
    </el-main>
  </el-container>
</template>
<script>
  // import {getUserMenus} from '@/api/index'
  import {mapActions, mapState} from 'vuex'
  export default {
    data () {
      return {
        activeIndex: '1',
        menus: []
      };
    },
    created () {
      if (window.localStorage.length > 0) {
        var string = window.localStorage.userInfo
        var userInformation = JSON.parse(string)
      }
      // this.getData();
    },
    computed: {
      ...mapState(['userInfo']),
      userName() {
        const string = window.localStorage.userInfo 
        const userInformation = JSON.parse(string)
        if (userInformation) {
          return userInformation.user.userName
        }
      }
    },
    methods: {
      ...mapActions(['sendUserInfo']),
      handleSelect () {
        
      },
      // async getData () {
      //   let data = await getUserMenus();
      //   this.menus = data && data.result;
      // },
      // 退出
      exit() {
        this.sendUserInfo(null);
        let islogout = true
        if (islogout) {
          this.$message({
            type: 'success',
            message: '退出成功'
          });
          this.$router.push('/');
        } else {
          this.$message({
            type: 'error',
            message: res.message
          });
        }
      }
    }
  }
</script>
<style lang="less">
  // @import './style.less';
  .el-header{
    padding: 0
  }
</style>
