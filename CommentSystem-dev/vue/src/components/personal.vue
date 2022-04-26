<template>
    <!--个人中心-->
    <el-button type="text" style="padding: 5px 5px" @click="drawer=true">
        <el-avatar :icon="UserFilled"></el-avatar>
    </el-button>
    <el-drawer v-model="drawer" class="footer" :with-header="false">
        <el-row >  <el-avatar :icon="UserFilled"
                              :size='number' style="margin: 0 auto"></el-avatar>
        </el-row >
        <el-row style="border-bottom: solid 1px #c6e2ff;" :gutter="2" >
            <el-col :span="6">
                <h3>账号</h3>
            </el-col>
            <!--这里要记得导入id-->
            <el-col :span="6">
                <h5 style="font-family: Arial">记得导入id</h5>
            </el-col>
        </el-row>
        <el-row  style="border-bottom: solid 1px #c6e2ff">
            <el-button type="text">
                个人中心
                <el-icon><avatar /></el-icon>
            </el-button>
        </el-row>
        <el-row style="border-bottom: solid 1px #c6e2ff">
            <el-button type="text">历史记录
                <el-icon><clock /></el-icon></el-button>

        </el-row>
        <el-row style="border-bottom: solid 1px #c6e2ff">
            <el-button type="text" >消息
                <el-icon><message /></el-icon></el-button>
        </el-row>
        <el-row :align="bottom">
            <el-col :span="12">  <el-button>
                退出
                <el-icon><arrow-right-bold /></el-icon>
            </el-button></el-col>
        </el-row>
    </el-drawer>

</template>

<script>
    import {ArrowRightBold, Avatar, Clock, Message,  UserFilled} from "@element-plus/icons-vue"
    import {ref} from "vue";
    export default {
        name: "personal-int",
        components:{ArrowRightBold,Avatar,Clock,Message,},
        data(){

            return{
                UserFilled,
                drawer:ref(false),
            }
        }

    }
</script>

<style scoped>

</style>