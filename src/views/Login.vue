<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <form  @submit.prevent="loginAPi">
          <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Email address</label>
            <input type="email" class="form-control" 
            id="exampleInputEmail1" aria-describedby="emailHelp"
            v-model="user.username"
            >
            <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
          </div>
          <div class="mb-3">
            <label for="exampleInputPassword1" class="form-label">Password</label>
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
        loginAPi(){
            const api = `${process.env.VUE_APP_API}admin/signin`;
            // 觸發post http 至後端
            // $http 為vue的方式
            this.$http.post(api,this.user)
            .then((res)=>{
                // 解構式存取  token, expired
                const { token, expired  } = res.data 
                console.log(token, expired);
                //MAD 儲存 cokie方式
                 document.cookie = `hexToken=${token};expires=${new Date(expired)};`; 

            })

           
        }
    }
}

</script>