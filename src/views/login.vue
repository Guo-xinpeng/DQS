<template>
  <div class="box">
    <div class="login">
      <el-input v-model="name" placeholder="请输入用户名"></el-input>
      <el-input v-model="pass" placeholder="请输入密码" type="password"></el-input>
      <el-button type="primary" @click="login">登录</el-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      pass: "",
    };
  },
  mounted() {},
  methods: {
    login() {
      this.$axios
        .post("https://www.liulongbin.top:8888/api/private/v1/login", {
          username: this.name,
          password: this.pass,
        })
        .then((res) => {
          console.log(res);

          this.$message({
            type: "info",
            message: res.data.meta.msg,
          });

          if (res.data.meta.status === 200) {
            localStorage.TOKEN = res.data.data.token;
            setTimeout(() => {
              this.$router.push("/about");
            }, 300);
          }
        });
    },
  },
};
</script>

<style>
.box {
  width: 100%;
  height: 100vh;
  /* background: rgb(176, 228, 235); */
}
.login {
  width: 25%;
  height: 39%;
  padding: 10px;
  background: #fff;
  display: flex;
  flex-direction: column;
  position: fixed;
  top: 30%;
  left: 34%;
}
.el-input {
  margin: 20px 0;
}
</style>