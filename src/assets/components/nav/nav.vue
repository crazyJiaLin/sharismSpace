<template>
    <div class="navigation-wrapper">
        <el-row type="flex" class="nav-row" justify="space-around">
            <el-col :span="4" v-for="(item,key) in routerList" :key="key" >
                <div class="router-link-wrapper">
                    <router-link class="router-link" :to="item.link">{{item.title}}</router-link>
                </div>
            </el-col>
        </el-row>
        <div class="nav-bottom-line"></div>
    </div>
</template>
    
<script>
    import './nav.css'
    export default{
        data() {
            return{
                routerList : [
                    {title:'博客管理',link:'/blog'},
                    // {title:'日志管理',link:'/journal'},
                    {title:'相册管理',link:'/album'},
                    {title:'文件管理',link:'/file'},
                    {title:'网站收藏',link:'/website'},
                    {title:'回收站',link:'/recyclebin'}
                    
                ],
                linkWidth : 0,
                linkOffsetLeft : 0,
                linkWrapperLeft : 0
            }
        },
        methods : {
            initLinkBottomLine(){
                let that = this;
                let timer = setTimeout(function(){
                    that.linkWidth = $('.navigation-wrapper .router-link.router-link-active').innerWidth();
                    that.linkOffsetLeft = $('.navigation-wrapper .router-link.router-link-active').offset().left;
                    // console.log(that.linkWidth)
                    // console.log(that.linkOffsetLeft)
                    that.linkWrapperLeft = $('.navigation-wrapper').offset().left
                    let dis = that.linkOffsetLeft - that.linkWrapperLeft;
                    $('.nav-bottom-line').css({
                        width : that.linkWidth,
                        left : dis
                    });
                },1000);
            },
            fixLinkBottomLine(){
                let that = this;
                that.linkWidth = $('.navigation-wrapper .router-link.router-link-active').innerWidth();
                that.linkOffsetLeft = $('.navigation-wrapper .router-link.router-link-active').offset().left;
                that.linkWrapperLeft = $('.navigation-wrapper').offset().left
                let dis = that.linkOffsetLeft - that.linkWrapperLeft;
                $('.nav-bottom-line').css({
                    width : that.linkWidth,
                    left : dis
                });
            }
        },
        mounted(){
            var that = this;
            that.initLinkBottomLine();
            $(window).resize(function(){
                that.fixLinkBottomLine();
            });
            $('.navigation-wrapper').on('click','.router-link',function(){
                that.linkWidth = $(this).innerWidth();
                that.linkOffsetLeft = $(this).offset().left;
                that.linkWrapperLeft = $('.navigation-wrapper').offset().left;
                var dis = that.linkOffsetLeft - that.linkWrapperLeft;
                // console.log(dis)
                $('.nav-bottom-line').css({
                    width : that.linkWidth,
                    left : dis
                })
            });
        }
    }

</script>
    