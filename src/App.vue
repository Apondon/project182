<template>
  <div id="app">
    <el-container>
      <el-header class='hdr'>
        <el-row :gutter="15">
          <el-col :span="6"><div class="logo">小莱书城</div></el-col>
          <el-col :span="18">
            <div class="top_button">
              <el-link  :underline="false" @click="loginVisiable = true">登录</el-link> |
              <el-link  :underline="false" @click="registVisiable = true">注册</el-link> |
              <el-link  :underline="false" @click="aboutVisiavle = true">关于</el-link>
            </div>
          </el-col>
        </el-row>
      </el-header>
      <el-main class="ctn">
        <div class="inner">
          <router-view/>
        </div>
      </el-main>
      <el-footer class="ftr">© 格莱科技集团 版权所有 Support by 软件研发部</el-footer>
    </el-container>
    <!-- 登录弹出框 -->
    
    <el-dialog :visible.sync="loginVisiable" @close="loginVisiable = false">
      <el-form :model="loginForm">
        <el-form-item label="账号" :label-width="formLabelWidth">
          <el-input v-model="loginForm.account" autocomplete="off" ></el-input>
        </el-form-item>
        <el-form-item label="密码" :label-width="formLabelWidth">
          <el-input v-model="loginForm.password" autocomplete="off" ></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="loginVisiable = false">登录</el-button>
      </span>
    </el-dialog>
    <!-- 注册弹出框 -->
    <el-dialog :visible.sync="registVisiable" @close="registVisiable = false">
      <el-form :model="registForm">
        <el-form-item label="账号" :label-width="formLabelWidth">
          <el-input v-model="registForm.account" autocomplete="off" ></el-input>
        </el-form-item>
        <el-form-item label="密码" :label-width="formLabelWidth">
          <el-input v-model="registForm.password" autocomplete="off" ></el-input>
        </el-form-item>
        <el-form-item label="确认密码" :label-width="formLabelWidth">
          <el-input v-model="registForm.cfmPsd" autocomplete="off" ></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="registVisiable = false">提交</el-button>
      </span>
    </el-dialog>
    <!-- 关于弹出框 -->
    <el-dialog :visible.sync="aboutVisiavle" @close="aboutVisiavle = false">
        <span>需要设置visible属性，它接收Boolean，当为true时显示 Dialog。Dialog 分为两个部分：body和footer，footer需要具名为footer的slot。title属性用于定义标题，它是可选的，默认值为空。最后，本例还展示了before-close的用法。</span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data(){
    return{
      // 登录
      loginVisiable:false,
      loginForm:{
        account:'',
        password:''
      },
      // 注册
      registVisiable:false,
      registForm:{
        account:'',
        password:'',
        cfmPsd:''
      },
      // 关于
      aboutVisiavle:false,
      // 自定义label宽度
      formLabelWidth: '80px'
    }
  }
}
</script>

<style lang="scss">
*{
  margin:0;
  padding: 0;
}
$lh:60px;
html,body{
  height: 100%;
}
body{
  margin: 0;
  padding: 0;

}
#app{
  height: 100%;
  section{
    height: 100%;
  }
}
.hdr{
  background: navy;
  .logo{
    line-height: $lh;
    font-size: 40px;
    color: #fff;
  }
  .top_button{
    text-align: right;
    line-height: $lh;
    color: #fff;
    span,a{
      color: #fff;
    }
  }
}
.ctn{
  background: oldlace;
  .inner{
    height: 100%;
    overflow-y: auto;
  }
}
.ftr{
  background: gainsboro;
  line-height: $lh;
  text-align: center;
  font-size: 12px;
  color: grey;
}
</style>
