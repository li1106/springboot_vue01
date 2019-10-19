<template>
    <el-main>
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/' }">学生管理</el-breadcrumb-item>
        <el-breadcrumb-item>详情</el-breadcrumb-item>
      </el-breadcrumb>
      <hr>
      <table class="el-table">
        <tr>
          <td>姓名</td>
          <td>{{detail.name}}</td>
        </tr>
        <tr>
          <td>生日</td>
          <td>{{detail.birthday}}</td>
        </tr>
        <tr>
          <td>头像</td>
          <td><img :src="detail.header_img" alt="" style="height: 128px;"></td>
        </tr>
        <tr>
          <td>地区</td>
          <td>{{detail.province_name}}/{{detail.city_name}}/{{detail.area_name}}</td>
        </tr>
        <tr>
          <td>说明</td>
          <td>{{detail.introduction}}</td>
        </tr>
      </table>
      <el-row>
        <el-button type="info" round @click="back">返回</el-button>
      </el-row>
    </el-main>
</template>

<script>
  const axios = require("axios");
  const baseUrl = "http://localhost:81";
    export default {
        name: "detail",
      data(){
        return{
          detail:{}
        }
      },
      methods:{
        back(){
          this.$router.push("/");
        }
      },
      created(){
        let params = this.$route.params;
        let self =  this;
        console.log(params);
        axios({
          url:baseUrl+"/student/detail",
          method:"get",
          params:{id:params.id}
        }).then((res)=>{
          console.log(res)
          self.detail = res.data.student;
        })
      }
    }
</script>

<style scoped>
  .demo-table-expand {
    font-size: 0;
  }
  .demo-table-expand label {
    width: 90px;
    color: #99a9bf;
  }
  .demo-table-expand .el-form-item {
    margin-right: 0;
    margin-bottom: 0;
    width: 50%;
  }
</style>
