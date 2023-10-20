<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <form  @submit.prevent="loginAPi">
          <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">登入Email 帳號</label>
            <input type="email" class="form-control" 
            id="exampleInputEmail1" aria-describedby="emailHelp"
            v-model="user.username"
            >
            <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
          </div>
          <div class="mb-3">
            <label for="exampleInputPassword1" class="form-label">登入 帳號密碼</label>
            <input type="password" class="form-control" id="exampleInputPassword1"
            v-model="user.password"
            >
          </div>
          <div class="mb-3 form-check">
            <input type="checkbox" class="form-check-input" id="exampleCheck1">
            <label class="form-check-label" for="exampleCheck1">Check me out</label>
          </div>
          <button type="submit" class="btn btn-primary"
         
          >Submit</button>
        </form>
      </div>

    </div>
  </div>

</template>

<script>
export default{
    data() {
        return {
            user:{
                username:'',
                password:'',
            }
        }
    },
    methods:{
        //登入方式 
        loginAPi(){
             // 組裝路徑方式
            const api = `${process.env.VUE_APP_API}admin/signin`;
            // 觸發post http 至後端
            // this.$http 為 axios 的方法
            this.$http.post(api,this.user)
            .then((res)=>{
              // 增加判斷 是否登入 轉跳
              if (res.data.success) {
                 console.log(res);
               // 解構式存取  token, expired
               const { token, expired } = res.data
               console.log(token, expired);
               //MAD 儲存 cokie方式
               document.cookie = `hexToken=${token};expires=${new Date(expired)};`;
                // 轉跳後台頁面 (產品頁面)
                this.$router.push('/dashboard/product')
              }
            })

           
        }
    }
}

</script>