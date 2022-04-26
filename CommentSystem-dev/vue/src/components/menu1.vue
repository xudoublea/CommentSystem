<template xmlns:el-col="http://www.w3.org/1999/html">
    <!--固定菜单-->
    <el-affix>
    <el-menu
            :default-active="activeIndex"

            mode="horizontal"
            @select="handleSelect"
            class="menu"
            >

        <!--logo标志-->
        <el-col :span="1">
        <el-image style="width: 50px; height: 50px;margin-right: 10px"
                  :src="logo"
        ></el-image>
        </el-col>
        <!--输入框-->
        <el-col :span="6" style="margin-right: 9cm;position: relative">
            <el-input class="i-input"
                      placeholder="Please Input"
            >
                <!--搜索标志-->
                <template #suffix>
                    <el-icon style="top: 10px"><Search /></el-icon>
                </template>
            </el-input>
        </el-col>
        <!--menu-->
        <el-menu-item index="1" style="color: #c45656; font-size: x-large"><a href="/classify">电影</a></el-menu-item>

        <el-menu-item index="2" style="color: #b88230 ;font-size: x-large">音乐</el-menu-item>
        <el-menu-item index="3" style="color: #3a8ee6;font-size: x-large">读书</el-menu-item>
        <el-menu-item index="4">登录</el-menu-item>
        <personal-int >
        </personal-int>

    </el-menu>
        </el-affix>
</template>

<script>

    import {Clock,Avatar,UserFilled,Search,ArrowRightBold,Message,} from '@element-plus/icons-vue'
    import {ref} from "vue";
    import cookie from "js-cookie";
    import PersonalInt from "./personal";
    export default {
        name: "menu-1",
        components: {PersonalInt},
        data(){
            return{
                Clock,
                Avatar,
                Message,
                Search,
                ArrowRightBold,
                UserFilled,
                activeIndex: '1',
                activeIndex2: '1',
                drawer:ref(false),
                logo:require("../assets/gallery/2.png"),
                username:''

            }
            },

        methods:{
            handleSelect(key, keyPath) {
                console.log(key, keyPath);
            },
          //头部显示登录信息
          getLogin() {
            let token = cookie.get('token');
            if (token) {
              this.username = cookie.get('username');
              console.log(this.username);
            }
          }
        },
      created() {
        this.getLogin()
      }
    }
</script>

<style scoped>
.el-drawer .el-row{
    margin-bottom: 12%;

}
    .menu{
        align-items: center;
    }
</style>