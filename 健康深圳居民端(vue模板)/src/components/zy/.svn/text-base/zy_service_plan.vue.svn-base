<template>
    <div class="app" style="overflow-x:hidden;height:100vh;background-color: #f2f2f2;">
        <div class="header">
            <mt-header title="服务计划">
                <a slot="left" @click='$router.push("/#")'>
                    <mt-button icon="back"></mt-button>
                </a>
                <a slot="right" @click='$router.push("/#")'>
                     <label>预约</label>
                </a>
            </mt-header>
        </div>
        <div class="session">
            <div class="tips">
                计划时间仅供参考，实际服务时间会有所出入，如有需要可以预约指定日期。
            </div>
            <div class="line"></div>
            <ul class="planList">
                <li>
                    <div class="axis_left">
                        <span class="served">已服务</span>
                    </div>              
                    <div class="axis_right cbafter">
                        <div class="fl">
                            <p class="planTime">计划时间：<span>2015-02-23</span></p>
                            <p class="serviceTime">服务时间：<span>2015-02-23</span></p>
                            <div class="serviceDetail"></div>
                        </div> 
                        <div class="fr">
                            <span class="commented">已评价</span>
                        </div>                        
                    </div>
                </li>
                <li>
                    <div class="axis_left">
                        <span class="noServe">待服务</span>
                    </div>              
                    <div class="axis_right cbafter">
                        <div class="fl">
                            <p class="planTime">计划时间：<span>2015-02-23</span></p>
                            <!-- <p class="serviceTime">服务时间：<span>2015-02-23</span></p> -->
                            <div class="serviceDetail">
                                <span class="noServeTip">待服务</span>
                            </div>
                        </div> 
                        <div class="fr">
                            <!-- <span class="goComment">评价</span> -->
                        </div>                        
                    </div>
                </li>
                <li>
                    <div class="axis_left">
                        <span class="served">已服务</span>
                    </div>              
                    <div class="axis_right cbafter">
                        <div class="fl">
                            <p class="planTime">计划时间：<span>2015-02-23</span></p>
                            <p class="serviceTime">服务时间：<span>2015-02-23</span></p>
                            <div class="serviceDetail"></div>
                        </div> 
                        <div class="fr">
                            <span class="goComment">评价</span>
                        </div>                        
                    </div>
                </li>
                <li>
                    <div class="axis_left">
                        <span class="served">已服务</span>
                    </div>              
                    <div class="axis_right cbafter">
                        <div class="fl">
                            <p class="planTime">计划时间：<span>2015-02-23</span></p>
                            <p class="serviceTime">服务时间：<span>2015-02-23</span></p>
                            <div class="serviceDetail">
                                <span class="order">预约</span>
                                <span class="warn">提醒</span>
                            </div>
                        </div> 
                        <div class="fr">
                            <span class="goComment">评价</span>
                        </div>                        
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
import md5 from 'md5'
import { Search,Cell } from 'mint-ui'
import {
    commonAjax,
    requestLoginon,
    areaAjax,dicAjax,commonAjaxKy
} from '../../api/api.js'
import {
    mapState,
    mapActions
} from 'vuex'
export default {
    data: function() {
        return {
            
        }
    },
    methods: {
        
    },
    mounted () {
        
    }
}
</script>

<style lang='stylus' scoped>
.header {
    position: fixed;
    z-index: 999;
    top: 0;
    left: 0;
    right: 0;
    .mint-header {
        height: 1rem;
        font-size: .4rem;
        background-color: #fff;
        color: #34b574;
    }
}
.session {
    margin-top: 1rem;
    .tips{
        background-color: #fffad0;
        color: #fe9d32;
        font-size: .25rem;
        padding: .2rem;
        line-height: .3rem;
        position: relative;
        z-index: 1;
    }
    .line{
        width:1px;
        height:100%;
        background-color:#e5e5e5;
        position:absolute;
        left: 20%;
        bottom: 0;
        top: 0;
        z-index: 0;
    }
    .planList li{
        position: relative;
        font-size: .3rem;
        width: 80%;
        padding: .3rem;
        margin-left: 20%;
        box-sizing: border-box;
        .axis_left{
            position: absolute;
            transform: translateX(-1.38rem);
            top: 30%;
            .served{
                color: #3a9a6c;
                padding-right: .35rem;
                background: url(../../assets/img/zy_point_g.png) no-repeat right;
                background-size: .25rem;
            }
            .noServe{
                color: #f89d28;
                padding-right: .35rem;
                background: url(../../assets/img/zy_point_y.png) no-repeat right;
                background-size: .25rem;
            }
        }
        .axis_right{
            background-color: #fff;
            padding: .3rem;
            border-radius: .1rem;
            .planTime{
                margin-bottom: .1rem;
            }
            .commented{
                font-size: .2rem;
                color: #d2d2d2;
                display: inline-block;
                padding: .15rem .2rem;
            }
            .goComment{
                font-size: .2rem;
                color: #fff;
                display: inline-block;
                padding: .15rem .2rem;
                border-radius: 3px;
                background-color: #f1c50e;
            }
            .serviceDetail{
                margin-top: .2rem;
                font-size: .2rem;
                .noServeTip{
                    color: #d2d2d2;
                }
                .order{
                    display: inline-block;
                    background-color: #52e99a;
                    border-radius: .2rem;
                    padding: .1rem .2rem;
                    color: #fff;
                }
                .warn{
                    display: inline-block;
                    background-color: #57c9fd;
                    border-radius: .2rem;
                    padding: .1rem .2rem;
                    color: #fff;
                }
            }
        }
    }
}
</style>
