<template>
 <div  class="common-layout">
     <el-container style="border-bottom: solid 1px #e6e6e6;height: 70px"
    >
         <!--菜单-->
         <el-header class="head">
              <el-row  class="row-style">
                  <!--logo-->
                 <el-col :span="2">
                     <el-image style="width: 50px; height: 50px;margin:0 10px"
                               :src="logo"
                     ></el-image>
                 </el-col>
                  <el-col :span="1">
                      <el-button type="text">
                       <div><a href="Layout">返回首页</a></div>
                      </el-button>
                  </el-col>
             <el-col
             :span="4">
             <h1 style="text-align: center;color: #c45656">电影</h1>
             </el-col>
             <el-col
             :span="8">
                 <!--搜索框-->
                 <el-input style="position: relative;flex:1 auto;" v-model="input" placeholder="Please input" />
             </el-col>
                  <el-col :span='3' style="margin-left: 60px;display: flex;">
                      <el-button type="text">
                      <el-icon class="icon-m" size="x-large"><message /></el-icon>
                      </el-button>
                      <el-button type="text">
                      <el-icon class="icon-m" size="x-large"><star/></el-icon>
                      </el-button>
                      <el-button type="text">
                      <el-icon class="icon-m" size="x-large"><clock/></el-icon>
                      </el-button>
                  </el-col>
                  <!--这里是头像框，因为我嫌头像框连带着个人中心的代码太多了，我就做成小组件了，记得导入-->
                  <el-col :span="3" style="margin-left: 70px">
                     <personal></personal>
                  </el-col>
              </el-row>
         </el-header>
         <el-container>
         <el-main class="main">
             <div style="margin: 0 auto;width: 600px;padding-bottom: 20px">
             <h1  class="ul" style="font-size: x-large;">选影视</h1>
             <div>
             <ul class="ul">
                 <li class="li" v-for="index in catelog" :key="index.id"  >
                     <span @mousemove="changecolor(index)" :class="{color:num===index,bac:catelogid===index.id}"
                          @click="clickchange(index)"
                          class="tag">{{index.catelogName}}</span>
                 </li>
             </ul>
             </div>
             <div>
                 <ul class="ul">
                     <li class="li" v-for="index in tag1" :key="index.id" :class="{bac:index[0]}">
                         <span  @mousemove="changecolor(index)" :class="{color:num===index,bac:tagid===index.id}"
                               @click="clickchange1(index)"
                                class="tag">{{index.tagName}}</span>
                     </li>
                 </ul>
             </div>
                 <div>
                     <ul class="ul">
                         <li class="li" v-for="index in Country" :key="index">
                         <span @mousemove="changecolor(index)"
                               :class="{color:num===index,bac:country===index}"
                               @click="clickchange2(index)"
                               class="tag">{{index}}</span>
                         </li>
                     </ul>
                 </div>
                 <div>
                     <ul class="ul">
                         <li class="li" v-for="index in time" :key="index">
                         <span @mousemove="changecolor(index)"
                               :class="{color:num===index,bac:Time===index}"
                               @click="clickchange3(index)"
                               class="tag">{{index}}</span>
                         </li>
                     </ul>
                 </div>
                 <!--
                 <div>
                     <el-select v-model="value" placeholder="选择分数区间">
                     <el-option>

                     </el-option>
                     </el-select>
                     <el-slider v-model="values" range max="10" show-stops :format-tooltip="formatTooltip"/>
                 </div>
                 -->
             </div>

             <!--作品图片-->
             <div style="width:600px;margin: 0 auto;">
                 <a href="Login">
                 <span v-for="index in worksList" :key="index" style="display: inline-block;margin-left: 10px">
                   <img :src="index.img"  class="imge"/>
                     <p>
                     <span class="name">{{index.name}}</span>
                         <span class="rate">{{index.name}}</span>
                     </p>
                     </span>
                 </a>
             </div>
             <div  style="text-align: center" v-show="totalnum===0">
                 <p>当前页面无搜索结果</p>
             </div>

         </el-main>
         </el-container>
     </el-container>
 </div>
</template>
<script>
    import {Clock, Message,  Star} from "@element-plus/icons-vue"
    import personal from "../components/personal";
    import request from "@/utils/request";
    import {ref} from "vue";
    export default {
        name: "movie-classify",
        components:{Message,Star, Clock, personal, },

       data() {

            return {

                logo: require("../assets/gallery/2.png"),
                tag1:[{id: 0, catelogName: '全部形式', tagcatelogId: '40'},],
                Country:[],
                time:[],
                catelog:[],
                num:0,
               Tag:'',
                Tag1:'',
              worksList:[],
                tagid:'',
                catelogid:'',
                country:'',
                Time:'',
                totalnum:'',
                value:ref(''),
                values:ref([0,10]),
                rate:'',





            }
        },
        //将自定义的body边距改为0px
        beforeCreate: function () {
            document.querySelector('body').setAttribute('style', 'margin:0;')
        },
      methods:{
            formatTooltip:function(val){
                         console.log(val)
                console.log("显示"+val)
                this.rate=val;
                         console.log(this.rate)
                console.log(this.values[0])
                console.log(this.values[1])
            },

            //鼠标移动到tag，tag变色
               changecolor:function (index) {
                this.num=index;
                   },
          //鼠标点击tag变色
          clickchange(index){
                   this.catelogid=index.id;
                   this.choose();
          },
          clickchange1(index){
            this.tagid=index.id;
            this.choose();
          },

          clickchange2(index){
              this.country=index;
              this.choose();
          },
          clickchange3(index){
            this.Time=index;
            this.choose();
          },

       choose(){
           request.get("/search/listPage?catelogId=40&tagcatelogId="+this.tagid+
               "&workscateId="+this.catelogid+"&country="+this.country+"&createTime="+this.Time).then(response =>{
               console.log(response)
               const res=response.worksList;
               this.worksList=res;
               console.log(res)
               this.totalnum=res.length
           })
       },
      Tags(){
                   request.get("/works/showSearchParam/40").then(response =>{
                       const data=response.data;
                       console.log(data);
                       this.tag1=data.tagList;
                       this.Country=data.country;
                       console.log(data.country)
                       this.time=data.createTime;
                       this.catelog=data.workscategories;
                   })
      }

      },
        mounted(){
            this.choose();
            this.Tags();
        },
    }

</script>

<style scoped>
    .common-layout{
       min-width: 1300px;
        max-width: 1300px;
        position: relative;
    }
    .head{
       width: 1280px;
        position: relative;

    }
    .head .row-style{
        position: relative;
        display: flex;
        align-items: center;
        margin: 0 auto;
    }

.icon-m{
    margin: 0 5px;
    color: black;
}

    .ul{
        display: inline-block;
        margin-bottom: 17px;
        width: 600px;
    }
    .tag{
        zoom: 1;
        cursor: pointer;
        font-size: 14px;
        padding: 2px 10px;
        line-height: 20px;
        border-radius: 2px;
        text-align: -webkit-match-parent;


    }
    .li{
        display: inline-block;

    }
  .el-main{
      width: 1024px;
      margin: 0 auto;
      flex: none;
  }
img{
    width:115px;
    padding-right: 20px;
 }
    p{
        overflow: hidden;
        line-height: 18px;
        padding-right: 15px;
        margin: 8px 0 20px;
    }
    .name{
        margin-right: 5px;
    }
    .rate{
        color: darkorange;
    }
    ul {
        display: block;
        list-style-type: disc;
       margin: 0;
        padding: 0;
    }
    .color:hover{

        color: #3a8ee6;
    }
    .bac{
        background-color: #c45656;
        color: white;
    }
    a{
        text-decoration: none;
        color: black;
    }
</style>
