<template>
  <div class="side-bar">
      <el-menu
          :collapse="isCollapse"
          active-text-color="#ffd04b"
          background-color="#334156"
          class="el-menu-vertical-demo"
          :default-active="getRoutePath"
          text-color="#fff"
          :router="true"
      >
        <el-menu-item index="/AdminPage/adminHome">
          <el-icon><House /></el-icon>
          <template #title>Home</template>
        </el-menu-item>
        <el-sub-menu index="/AdminPage/platGeneralInfo">
          <template #title>
            <el-icon><Food /></el-icon>
            <span>Plat</span>
          </template>
          <el-menu-item index="/AdminPage/platGeneralInfo">General Info</el-menu-item>
          <el-menu-item index="/AdminPage/platSimpleChange">Edit Plat</el-menu-item>
          <el-menu-item index="/AdminPage/platChange">Add Plat</el-menu-item>
          <el-menu-item index="/AdminPage/platDeleteHistory">Inactive List</el-menu-item>
        </el-sub-menu>
        <el-sub-menu index="/AdminPage/newsInfo">
          <template #title>
            <el-icon><Notification /></el-icon>
            <span>News</span>
          </template>
          <el-menu-item index="/AdminPage/newsInfo">Edit News</el-menu-item>
          <el-menu-item index="/AdminPage/addNews">Add News</el-menu-item>
        </el-sub-menu>
        <el-menu-item index="/AdminPage/personInfo" :disabled="!showPersonPage">
          <el-icon><User /></el-icon>
          <template #title>Personnel management</template>
        </el-menu-item>
      </el-menu>
  </div>
</template>

<script>
import {adminRoleId} from "@/utils/const/const";

export default {
  name: "AdminSidebar",
  data() {
    return {

    }
  },
  computed:{
    /**
     * @description: get current route path, without parameters
     * @author yuan.cao@utbm.fr
     * @date 2022-05-14 21:35:34
     */
    // getRoutePathNoParam(){
    //   const interrogationPos = this.$route.path.indexOf('?');
    //   const withParam = interrogationPos!==-1;
    //   let pathBrut = '';
    //   if(withParam){
    //     pathBrut = this.$route.path.substring(0,interrogationPos);
    //   }else{
    //     pathBrut = this.$route.path
    //   }
    //   console.log(pathBrut);
    //   console.log(this.$route.path);
    //   return pathBrut;
    // },
    isCollapse(){
      return this.$store.getters.collapseForAdmin
    },
    getRoutePath(){
      return this.$route.path;
    },
    //this determines if this person has the right to access Personnel Management Page
    showPersonPage(){
      const type = typeof (this.$store.getters.role)
      if(type==="number"){
        return this.$store.getters.role===adminRoleId
      }else{
        //parse proxy
        const roleObj = JSON.parse(JSON.stringify(this.$store.getters.role))
        return roleObj.role===adminRoleId
      }
    }
  },
  methods:{


  }
}
</script>

<style scoped>
.side-bar{
  height: 100%;
  background-color: #334156;
}
.el-menu-item,>>> .el-submenu__title {
}
</style>