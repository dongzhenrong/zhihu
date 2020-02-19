<template>
<div>
    <div class="img">
        <img :src="main.image" width="100%" height="380px"> 
        <div class="title">{{main.title}}</div>
        <div class="img_source">{{main.image_source}}</div>
    </div>
    <div v-html="main.body" class="text"></div>
    <!-- <div id="footer">
        <div><img src="@/assets/img/back.png" width="30rem" height="30rem" class="one" @click="hrefone"></div>
        <div><img src="@/assets/img/msg.png" width="30rem" height="30rem" class="second" @click="hreftwo"></div>
        <div><img src="@/assets/img/zan.png" width="30rem" height="30rem"></div>
        
        <div class="praise">
            <span id="praise"><img src="@/assets/img/zan.png" id="praise-img" class="animation"></span>
            <span id="praise-txt" class="">89</span>
            <span id="add-num" style="display: inline;"><em class="add-animation">-1</em></span>
        </div>
        <div><img src="@/assets/imgouc.png" width="33rem"></div>
        <div @click="shareToRoom()"><img src="@/assets/img/zhuanf.png" width="30rem" height="30rem" class="last"></div>
    </div> -->
    <div class="footer">
        <div class="back">
            <img src="@/assets/images/left.png" width="30rem" height="30rem" @click="hrefone">
        </div>
        <div class="message">
            <img src="@/assets/images/man.png" width="30rem" height="30rem" @click="hreftwo">
            <span>{{comments}}</span>
        </div>
        <div class="good">
            <img src="@/assets/images/man.png" width="30rem" height="30rem" @click.once="goodSum">
            <span>{{popularity}}</span>
        </div>
        <div class="collect">
            <img :src=" imgsrc || require('@/assets/images/man.png')" width="30rem" height="30rem" @click="collect">
        </div>
        <div class="share">
            <img src="@/assets/images/man.png" width="30rem" height="30rem" @click="sharePoper">
        </div>
    </div>
    <div class="poper" >
        <div :class="{poperBg:ifpoperCupHiden}" @click="sharePoperClose"></div>
        <div class="poperArea" :class="{poperCupHiden:ifpoperCupHiden}">
            <div>
                <img src="@/assets/images/man.png">
                微信好友
            </div>
            <div>
                <img src="@/assets/images/man.png">
                朋友圈
            </div>
            <div>
                <img src="@/assets/images/man.png">
                新浪微博
            </div>
            <div>
                <img src="@/assets/images/man.png">
                QQ
            </div>
            <div>
                <img src="@/assets/images/man.png">
                复制链接
            </div>
            <div>
                <img src="@/assets/images/man.png">
                浏览器打开
            </div>
            <div>
                <img src="@/assets/images/man.png">
                更多
            </div>
        </div>   
    </div>
</div>
</template>

<script>
export default {
name: 'productdetailspage',
methods: {
        hrefone() {
            this.$router.replace('/');
        },
        hreftwo() {
            this.$router.replace('/comment');
        },
        collect(){
            if(this.imgsrc){
               this.imgsrc = '';
            }else{
                this.imgsrc = require('@/assets/images/man.png')
            }
        },
        goodSum(){
            this.popularity++;
        },
        goComments(){
            this.$router.push(`/comments?comments=${this.comments}&longComments=${this.long_comments}&shortComments=${this.short_comments}&id=${this.id}`)
        },
        sharePoper(){
            this.ifpoperCupHiden = true;
        },
        sharePoperClose(){
            this.ifpoperCupHiden = false;
        }
    },

mounted(){
        this.id = this.$route.params.id
        this.axios.get(`news/3892357`).then(res => {
            this.main = res.data
        })
         this.axios.get(`story-extra/${this.id}`).then(res => {
            this.comments = res.data.comments;
            this.popularity = res.data.popularity;
            this.long_comments = res.data.long_comments;
            this.short_comments = res.data.short_comments;
        })
    },

data() {
    return {
    id:'',
    main:'',
    comments:'',
    popularity:'',
    imgsrc:'',
    long_comments:'',
    short_comments:'',
    ifpoperCupHiden:false,
    }
  }
}
</script>
<style>
.main{
    width: 96%;
    box-sizing: border-box;
    padding-left: 1.2rem;
    margin-top: 1rem
}
.img{
    position: relative;
}
.question-title{
     width: 90%;
     padding-left: 1.3rem;
}
.answer{
    width: 90%;
    padding-left: 1.3rem;
    margin-top: 1rem
}
.answer p{
    margin-top: .8rem;
    font-size: 1.1rem
}
.img .title{
    position: absolute;
    left: 1rem;
    bottom: 4rem;
    color: #fff;
    font-size: 1.5rem;
    font-weight: bold;
}
.img .img_source{
    position: absolute;
    bottom: 1rem;
    right:1rem;
    color: #fff;
    font-size: 0.8rem
}
.view-more a{
    color: #fff
}
.view-more{
    margin-bottom: 4rem;
    background-color: #1D82FE;
    border: 0;
    outline: 0;
    height: 3rem;
    border-radius: 1.5rem;
    width: 23rem;
    line-height: 3rem;
    font-size: 0.8rem;
    text-align: center;
    margin-left: 1.3rem;
    margin-top: 1rem
}
.text img{
    width: 90%
}
.text .avatar{
    width: 2.5rem
}
.footer{
    display: flex;
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    background-color: #eee;
    padding: 6px 0;
}
.footer div{
    flex: 1;
    display: flex;
    justify-content: center
}
.footer div.back{
    border-right: 1px solid #ccc;
}
.message,.good{
    position: relative;
}
.message span,.good span{
    position: absolute;
    top: 0;
    right: 0;
    font-size: 12px
}
.poperBg{
    position: fixed;
    top: 0;
    left: 0;
    background-color:rgba(0,0,0,0.6);
    height: 100%;
    width: 100%;
    z-index: 1200;
}
.poper img{
    width: 50px;
    height:50px;
    margin-bottom: 3px;
}
.poperArea{
    width: 100vw;
    display: flex;
    flex-wrap: wrap;
    padding:26px 12px;
    box-sizing: border-box;
    background-color: #fff;
    border-top-right-radius: 20px;
    border-top-left-radius: 20px;
    position: fixed;
    bottom: 0;
    left: 0;
    z-index: 1600;
    transition: all 0.3s ease;
    transform:translateY(100%) 
}
.poperArea div{
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 25%;
    box-sizing: border-box;
    margin-bottom: 16px;
}
.poperCupHiden{
    transform:translateY(0%) 
}
.back img{
    width: 36%
}
.text .avatar{width: 50px}
</style>