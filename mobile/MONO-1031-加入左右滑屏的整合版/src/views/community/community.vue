<template>
  <div class="cummunity">
        <div class="club">
            <h2 class="fl">社区</h2>
            <i class="fa fr fa-plus" aria-hidden="true"></i>
        </div>
        <div class="seek">
            <input type="text" value="搜索你感兴趣的内容"/>
            <i class="fa fa-search" aria-hidden="true"></i>					
        </div>
        <div class="special">
            <h2 class="clearfix more">
                <span class="fl">热门小组、活动</span>
                <span class="fr">
                    <router-link tag="a" to="/Un">查看全部</router-link>
                </span>
            </h2>
            <div class="theme clearfix">
                <div v-for="item in this.$store.state.comunityData.hotActive" @click="showPosition('top')">
                    <img :src="item" />
                    <!-- <p class="same-title">24小时电影院</p>
                    <p class="person-num"><span>1234</span>人</p> -->
                </div>                
            </div>
            <toast v-model="showPositionValue" type="text" :time="800" text="玩脱了，页面找不到了" :position="position"></toast>
        </div>
        <div class="more-groups">
            <h3>我参加的小组和活动</h3>
            <p @click="showPosition('middle')">还美参加任何小组和活动，点我发现更多<br>/^-^/</p>
        </div>
        <!-- <div class="slideshow">
            <img src="img/show1.png" />
            <div class="circle">
                <div class="white"></div>
                <div></div>
            </div>
        </div> -->
        <div class="slideshow">
            <slide-show></slide-show>
        </div>
        <div class="diff-theme">
            <div class="theme clearfix">
                <div  v-for="item in this.$store.state.comunityData.comunityTheme" @click="showPosition('bottom')">
                    <img :src="item" />
                    <!-- <p class="same-title">24小时电影院</p>
                    <p class="person-num"><span>1234</span>人</p> -->
                </div>
            </div>
        </div>	
        <Footer-nav></Footer-nav>			
    </div>
</template>

<script>
    import {Toast} from 'vux'
    import FooterNav from '@/components/footer/footer'
    import SlideShow from '@/components/slide-show/slide-show'
    import Axios from 'axios'
    import api from '@/api/api.js' // 请求数据的文件

    export default {
        components:{
            FooterNav,
            SlideShow,
            Toast
        },
        data () {
            return {
                position: 'default',
                showPositionValue: false
            }
        },
        methods:{
            showPosition (position) {
                this.position = position
                this.showPositionValue = true
            },
            getComunityData(){
                api.getComunityData().then((data) => {
                    // console.log(data.data.data.list)
                    this.$store.commit('changeComunityData',data.data.data.list)
                })
            }
        },
        mounted() { 
            this.getComunityData()
        }
    }
</script>
