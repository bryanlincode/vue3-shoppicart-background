<template>
     <Navbar></Navbar>
      <div class="container-fluid">
          <router-view/>
      </div>
</template>

<script>
import Navbar from '../components/Navbar.vue';

export default {
      components:{
        Navbar
      },
      created() {
        //生命週期取得
        const token = document.cookie.replace(
            /(?:(?:^|.*;\s*)hexToken\s*=\s*([^;]*).*$)|^.*$/,
            "$1",
        );
        // 使用axios htpp 儲存 Authorization
        this.$http.defaults.headers.common['Authorization'] = token;
        // 驗證登入狀況
        const api = `${process.env.VUE_APP_API}api/user/check`;
        this.$http.post(api, this.user)
            .then((res) => {
                if (!res.data.success) {
                    // 如果失去 cookie 就轉跳回去登陸頁面
                    this.$router.push('/login')
                }
               console.log(res);
               console.log('this',this);
            })
    }
}
</script>
