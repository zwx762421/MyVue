<template>

<!-- vue的模板里面 所有的内容要被一个根节点包含起来  -->

  <div id="app">  
    
    <!--<h2>{{msg}}</h2>

    <input type="text" v-model='msg'>



    <button v-on:click="getMsg()">获取表单里面的数据get</button>

    <button v-on:click="setMsg()">获取表单的数据set</button>

    <hr>
    <br>
    <input type="text" ref="userinfo">
    <br>
    <br>
    <div ref="box">我是一个box</div>

    <button v-on:click="getInputValue()">获取第二个表单里的数据</button>-->


    <input type="text" ref="userId" placeholder="用户名：">
    <br>
    <input type="password" class="password" ref="passWord" placeholder="密码">
    <br>
    <button v-on:click="login()">登录</button>


  </div>
</template>

<script>
  //双向数据绑定 MVVM vue就是一个MVVM框架。
  /**
   * M model
   * v view
   * MVVM  model改变会影响视图，视图改变反过来影响model
   *
   * 双向数据绑定必须在表单使用
   */
  import Axios from 'axios'
    export default {
      data () {  /*业务逻辑里面定义的数据*/
        return {
          //msg:'你好vue'
        }
      },
      methods:{
        /*getMsg(){
          //alert('方法执行')
          //方法里面获取data里面的数据
          alert(this.msg)
        },
        setMsg(){
          this.msg = "我是改变后的数据";
        },
        getInputValue(){
          //获取ref定义的dom节点
          console.log(this.$refs.userinfo);
          var password = this.$refs.userinfo.value;
          //alert(password);
          alert(this.$refs.box.style.background='red');
        }*/
        login(){
          var userId = this.$refs.userId.value;
          var passWord = this.$refs.passWord.value;
          var sendMessage = '{"userId":"'+userId+'","passWord":"'+passWord+'"}'.toString();
          var jsonRequest = JSON.parse(sendMessage);
          var api = "http://localhost:9999/Myself/userinfo/userLogin";
          //请求数据
          Axios.post(api,jsonRequest).then(function (response) {
            console.info(response);
            if(response.data.data == userId && response.data.status == "200"){
              alert("登陆成功！");
            }else {
              alert("登陆失败！");
            }
          },function (err) {
            console.log(err)
          })
        }
      }

    }
</script>


<style lang="scss">

</style>
