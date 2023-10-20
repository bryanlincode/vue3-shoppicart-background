<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Navbar</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Features</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#" @click.prevent="loginOut">登出</a>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled">Disabled</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>


<script>
  export default {
    methods: {
        // 登出功能
      loginOut() {
        // 組裝路徑方式
        const api = `${process.env.VUE_APP_API}logout`;
        // 觸發post http 至後端
        // this.$http 為 axios 的方法
        this.$http.post(api,this.user)
          .then((res) => {
            // 增加判斷 是否登入 轉跳
            if (res.data.success) {
              console.log(res);
              this.$router.push('/login')
            }
          })
      }
    }
  }
</script>