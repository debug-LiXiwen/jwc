<template>
  <div>
    <el-container class="con">
      <el-header class="header" height="80px">
        <el-row>
          <el-col :span="12"><div class="grid-content bg-purple"><img src="../assets/headLogo.png" class="header-logo"/> </div></el-col>
          <el-col :span="12"><div class="grid-content bg-purple-light text-right">
           <span ><i class="el-icon-share i_rd"></i><span @click="exit">安全退出</span></span>
          </div></el-col>
        </el-row>
      </el-header>
      <el-container>
        <el-aside width="220px" class="aside">
          <el-menu  router :default-active="$route.path"
                    background-color="#dbe9f1"
                    active-text-color="#6ec673" id="menu"
                    >
            <el-submenu index="4">
              <template slot="title"><i class="el-icon-location"></i>评估结果统计</template>
              <el-menu-item-group >
                <el-menu-item index="/show"><i class="el-icon-tickets"></i>评估结果展示</el-menu-item>
              
              
              </el-menu-item-group>
            </el-submenu>
           
            <el-submenu index="8">
              <template slot="title"><i class="el-icon-location"></i>项目管理</template>
              <el-menu-item-group>
                 <el-menu-item index="/newActivity"> <i class="el-icon-tickets"></i>新增活动</el-menu-item>
                <el-menu-item index="/manage"> <i class="el-icon-tickets"></i>活动管理</el-menu-item>
                <el-menu-item index="/addActivity"> <i class="el-icon-tickets"></i>活动项目添加</el-menu-item>
                <el-menu-item index="/manageActivity"> <i class="el-icon-tickets"></i>活动项目管理</el-menu-item>
               
               

              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="9">
              <template slot="title"><i class="el-icon-location"></i>用户管理</template>
              <el-menu-item-group>
                <el-menu-item index="/newUser"><i class="el-icon-tickets"></i>新增用户</el-menu-item>
                <el-menu-item index="/manageUser"><i class="el-icon-tickets"></i>用户信息管理</el-menu-item>
              

              </el-menu-item-group>
            </el-submenu>

            </el-menu>

        </el-aside>
                   <el-card id="card" class="box-card">
              <div slot="header" class="clearfix">
                <span>新增用户</span> 
              </div>
              <div class="item">
              姓名：<el-input class="nu" v-model="name" placeholder="请输入内容"></el-input>
               </div><div class="item">
               账号：<el-input class="nu" v-model="phone" placeholder="请输入内容"></el-input>
              </div><div class="item">
                密码：<el-input class="nu" v-model="password" placeholder="请输入内容"></el-input>
              </div><div class="item">
               单位：<el-input class="nu" v-model="unit" placeholder="请输入内容"></el-input>
              </div>
              <div id='btn'>
               <el-button id="button"  type="primary" plain @click="add">确定</el-button>
               </div>
            </el-card>
      </el-container>
    </el-container>
  </div>
</template>

<script>
export default {
  data(){
    return{
      name:"",
      phone:"",
      unit:"",
      password:""
    }
  },
  mounted(){

  },
  methods: {
    exit: function () {
      var that = this;
             this.$axios.get('/logout', {

  })
  .then(function (response) {
    console.log(response);
      if (response.data.resultCode === 200) {
        sessionStorage.clear()
        that.$message({
            message: '退出成功',
            type: 'success',
            duration: 2000
          })
          that.$router.push('/')
       
        } else {
          that.$router.push('/')
        }
  })
  .catch(function (error) {
    console.log(error);
  });
    } ,
     add:function(){     
       var that = this;  
      this.$axios({
      data: {
        unit:this.unit,
      userName:this.name,
      phone:this.phone,
      password:this.password
      },
      method:'post',
    url:'/register ',
    headers: {
            'Content-Type': 'application/json',
      }
  })
  .then(function (response) {
    console.log(response.data.resultCode);
      if (response.data.resultCode === 200) {
          that.$message({
            message: '添加成功',
            type: 'success',
            duration: 2000
          })
       
        } else {
          that.$message({
             message: response.data.message,
            type: 'error',
            duration: 2000
          })
        }
  })
  .catch(function (error) {
    console.log(error);
  });
   }
    },
    handleClose(tag) {
      this.dynamicTags.splice(this.dynamicTags.indexOf(tag), 1);
    },
 
  }

</script>

<style>
#btn{
  margin:5% auto;
  width:68px;
}
.item{

  text-align:center; 
}
.nu{
  width: 70%;
  margin: 1%;
}
  #card{
    margin:3% auto;
  }
  .text {
    font-size: 14px;
  }

  .item {
    margin-bottom: 18px;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both
  }

  .box-card {
    width: 480px;
  }
a{
  text-decoration:none; 
  color:rgb(21, 46, 112);
}
.con{
  width: 100%;
  height: 100%;
  position: absolute;
}
*{
  margin: 0; padding: 0;
}
.test{
  width: 500px;
  height: 500px;
  background-color: red;
}
.header{
  width: 100%;


  background-repeat: no-repeat;
  background-size: 100% 100%;
  color: #ffffff;
  background-color:#0d3349 ;
}
  .header-logo{
    margin-top: 8px;
    height: 64px;
  }
  .text-right{
    text-align: right;
    line-height: 80px;
  }
  .text-right span{
    margin-right: 10px;
  }
  .text-right span i{
    margin-right: 5px;
  }

  .aside{
    background-color: rgba(219, 233, 241, 0.45);
  }
  .el-submenu{
    border-bottom: 1px solid #bbe0f6;

  }
  .mean-top{
    width: 100%;
    height: 41px;
    line-height: 41px;
    text-indent: 5px;
  }
  .main{
    background-color: #eeeeee;
    width: 100%;
    padding: 0px;
  }
  .main-tab{
    width: 100%;
    line-height: 40px;
    border-bottom: 2px solid #0d3349;
    height: 40px;
  }

</style>
