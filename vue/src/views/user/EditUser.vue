<template>
  <div style="width: 80%">
    <div style="margin-bottom: 30px">新增用户</div>
    <el-form :inline="true" :model="form"  label-width="120px">
      <el-form-item label="姓名">
        <el-input v-model="form.name" placeholder="请输入姓名"></el-input>
      </el-form-item>

      <el-form-item label="年龄">
        <el-input v-model="form.age" placeholder="请输入年龄"></el-input>
      </el-form-item>
      <el-form-item label="性别">
        <el-input v-model="form.sex" placeholder="请输入性别"></el-input>
      </el-form-item>
      <el-form-item label="联系方式">
        <el-input v-model="form.phone" placeholder="请输入联系方式"></el-input>
      </el-form-item>
      <el-form-item label="地址">
        <el-input v-model="form.address" placeholder="请输入地址"></el-input>
      </el-form-item>
    </el-form>

    <div style="text-align: center; margin-top: 30px">
      <el-button type="primary" @click="save" size="medium">提交</el-button>
      <!--<el-button type="danger">返回列表</el-button>-->
    </div>
  </div>
</template>

<script>
import request from "@/utils/request";
export default {
  name: 'AddUser',
  data() {
    return {
      form:{}
    }
  },
  methods:{
    save() {
      request.post('/user/save', this.form).then(res =>{
        if(res.code === '200'){
          this.$notify.success('新增成功')
          this.form = {}
        }else{
          this.$notify.error(res.msg)
        }
      })
    }
  }
}
</script>
