<template>
    dashboard
</template>




<script>
export default {
      created() {
        const token = document.cookie.replace(
            /(?:(?:^|.*;\s*)hexToken\s*=\s*([^;]*).*$)|^.*$/,
            "$1",
        );
        console.log('dashboard', token);
        console.log('1');
        // 使用axios htpp 儲存 Authorization
        this.$http.defaults.headers.common['Authorization'] = token;
        // 確認登入狀況
        const api = `${process.env.VUE_APP_API}api/user/check`;
        this.$http.post(api, this.user)
            .then((res) => {
               console.log(res);
            })
    }
}
</script>
