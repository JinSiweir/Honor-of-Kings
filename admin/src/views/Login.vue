<template>
  <div class="login-container">
    <el-card class="login-card" header="请先登录">
      <el-form @submit.prevent="login">
        <el-form-item label="用户名">
          <el-input v-model="model.username"> </el-input>
        </el-form-item>
        <el-form-item label="密码">
          <el-input v-model="model.password" type="password"> </el-input>
        </el-form-item>

        <el-form-item class="login-button">
          <el-button type="primary" native-type="submit">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      model: {},
    };
  },
  methods: {
    async login() {
      const res = await this.$http.post("login", this.model);
      localStorage.token = res.data.token;
      this.$router.push("/");
      this.$message({
        type: "success",
        message: "登录成功",
      });
    },
  },
};
</script>

<style>
.login-container {
  display: flex;
  justify-content: center;
}
.login-card {
  width: 25rem;
  margin: 6rem;
}
.login-button {
  display: flex;
  justify-content: center;
}
</style>
