<template>
    <div class="demo-image">
        <el-row style="margin-top: 10%">
            <el-col v-for="it in pictureurls"
                    :key="it"
                    :span="6"
                    :offset="it>0?2:0">
                <el-card >
                    <img
                            :src="it.path"
                            class="block"
                    />
                    <span class="demonstration">{{it.name}}</span>
                </el-card>
            </el-col>
        </el-row>
        <div >
            <el-pagination
                    v-model:currentPage="pageCurrent"
                    v-model:page-size="pageSize"
                    layout="prev, pager, next, jumper"
                    :total="musictotal"
                    @size-change="handleSizeChange"
                    @current-change="handleCurrentChange"
                    class="demo-pagination-block"
            />
            <div class="demonstration">共{{musicPages}}页，共有{{ musictotal}}首音乐</div>
        </div>
    </div>
</template>

<script>

    import request from "@/utils/request";



    export default {

        name: "mid-pic",

        data(){
            return{
                //电影名字，评分，图片地址
                pictureurls:[],
                ImgUrl:[],

                //总数据条数


                //当前页码
                pageCurrent:1,
                //每页条数
                pageSize: 6,
                //总页数
                musicPages:2,
                musictotal:'',


            }
        },


        methods:{
            getInfo(){      //首页展示影片

                request.get("/works/indexshow?pageCurrent=" + this.pageCurrent + "&pageSize=" + this.pageSize).then(data =>{
                    const res = data.data;
                    console.log(data.data)
                    const movieURL = res.music;
                    console.log(res.music)
                    this.pictureurls = movieURL;
                    console.log(res.movieTotal);
                    this.musictotal=res.musicTotal;

                })
            },


            handleCurrentChange(page){
                this.currentPage = page;
                console.log(this.currentPage);
                this.getInfo();
            },

            handleSizeChange(size){
                this.pageSize = size;
                console.log(this.pageSize);
                this.getInfo();
            },





        },

        //生命周期：挂载完成，可以访问当前this实例
        mounted() {
            this.getInfo();
            //  this.getImage();
        },


    }
</script>

<style scoped>
    .demo-image .block {
        display: inline-block;
        width: 100%;
        object-fit: scale-down;
        height: 170px;
    }
    .demo-image .demonstration {
        display: block;
        color: var(--el-text-color-secondary);
        font-size: 14px;
        text-align: center;
        margin-top: 20px;
        margin-bottom: 20px;
    }
    .demo-pagination-block{
        margin: auto;
        width: 40%;
        position: relative;


    }

</style>