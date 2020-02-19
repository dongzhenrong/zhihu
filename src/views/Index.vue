<template>
    <div>
        <div id="head">
            <div class="left">
                <p class="six">{{day}}</p>
                <p class="two">{{month}}月</p>
            </div>
            <div class="middle">
                <div class="mleft"><img src="@/assets/images/shu.png" alt="" height="55rpx" width="20rpx"></div>
            </div>
            <div class="hello">{{ sayHao }}</div>
            <div class="right"><img src="@/assets/images/man.png" width="40rpx" height="40rpx"></div>
        </div>
        <div class="banner">
            <van-pull-refresh>
                <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
                    <van-swipe-item v-for="item in swiperList" :key="item.id" @click="go">
                        <a :href="item.url">
                            <img :src="item.image" width="100%" height="400rpx">
                            <p>
                                {{item.title}}
                                <span>{{item.hint}}</span>
                            </p>
                        </a>
                    </van-swipe-item>
                </van-swipe>
            </van-pull-refresh>
        </div>
        <div id="con">
            <a :href="item.url" v-for="item in conList" :key="item.id" @click="go">
                <p>
                    {{item.title}}<br />
                    <span >{{item.hint}}</span>
                </p>
                <img :src="item.images" width="100rem" height="100rem">
            </a>
        </div>
    </div>
</template>
<style>
*{margin: 0;padding: 0}
.hello{
    font-weight: bold;
    font-size: 24rpx;
    align-items: center;
    text-indent: 0.5em;
}
#head{overflow: hidden;width: 100%}
#head .left{margin-left: 0.5rem}
#head .left,.middle{float:left;}
#head .right{float:right;padding: 0.5rem 1rem 0 0}
#head .left p{text-align: center}
#head .left .six{font-size: 1.5rem;font-weight: bold}
#head .left .two{font-size: 1.1rem}
#head .middle .mleft,#head .mright{float: left;}
#head  .mright{font-size: 1.8rem;padding-top: 0.5rem;padding-left: 0.1rem}
.banner{width: 100%;overflow: hidden;}
.banner a{color: #fff;}
.banner p{width:95%;position:absolute;bottom:24px;color: #fff;text-align: left;padding-left:1rem;}
#con a{display: block;padding-bottom: 8rem;padding-left: 0.5rem;color: black;font-size: 1.1rem}
#con img{float: right;padding-right: 0.5rem}
#con p{float: left;width: 70%}
#con  a span{color:#e9e9e9;font-size: 0.8rem}
</style>
<script>
import Vue from 'vue';
import { Swipe, SwipeItem } from 'vant';

Vue.use(Swipe);
Vue.use(SwipeItem);

export default{
    
    components: {

    },
    data(){
        return {
            day:'',
            month:'',
            sayHao:'',
            swiperList: [],
            conList: []
        }
    },
    methods: {
        go() {
            this.$router.replace('/Details');
        }
    },
    mounted:function(){
        this.axios.get("news/latest").then(res => {
            this.swiperList = res.data.top_stories;
            this.conList = res.data.stories
        })
        this.day = getNowDate().getDate();
       this.month = getNowDate().getMonth()+1;
       let sayHao = getNowDate().getHours();
       switch(sayHao){
            case 0:;
            case 1:;
            case 2:;
            case 3:;
            case 4:;
            case 5:;
            case 6:;
            case 7:;
            case 8 : this.sayHao = '早上好' ; break;
            case 9:;
            case 10:;
            case 11:;
            case 12:;
            case 13 : this.sayHao = '中午好' ; break;
            case 14:;
            case 15:;
            case 16:;
            case 17:;
            case 18:;
            case 19 : this.sayHao = '下午好' ; break;
            case 20:;
            case 21:;
            case 22:;
            case 23 : this.sayHao = '晚上好' ; break;
       }
    },
}
var getNowDate = function(){
    return new Date();
}
</script>