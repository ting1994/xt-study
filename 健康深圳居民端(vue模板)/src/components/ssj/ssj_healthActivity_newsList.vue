<template>
    <div class="app" style="overflow-x:hidden;height:100vh;background-color: #fafafa;">
       <div class="header">
            <mt-header title="健康活动">
                <a slot="left" @click='$router.push("/xie_xiaoxi")'>
                    <mt-button icon="back"></mt-button>
                </a>
            </mt-header>
        </div>
        <div class="session">
            <ul class="msgList">
                <li class="cbafter" v-for="(item,index) in msgDetail">
                    <p class="msgTime">{{item.sendTime}}</p>
                    <div class="msgContent">
                    	<h3>健康讲座通知</h3>
                        <span>{{item.content}}</span>
                        <b>查看详情</b>
                    </div>
                </li>
            </ul>
            <div id="more" v-show="this.msgDetail.length>=10" class="more" @click="showMore()">查看更多</div>
        </div>
    </div>
</template>
<script>
import md5 from 'md5'
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
            msgDetail: [],
            businessType: '002',
            pageNo: 1,
            maxDisplayLength: 10
        }
    },
    methods: {
        showMore(){
            this.pageNo++
            let params = ["",this.businessType,this.pageNo,this.maxDisplayLength]
            commonAjaxKy(JSON.stringify(params), 'hcn.notification', 'getAllNotifications').then(res => {
                if (res.code === 200) {
                    this.msgDetail = this.msgDetail.concat(res.body)
                    // console.log(this.msgDetail)
                    if(res.body < 10){
                        document.getElementById('more').style.display = 'none'
                    }
                }
            })
        }
    },
    mounted() {
        let params = ["",this.businessType,this.pageNo,this.maxDisplayLength]
        commonAjaxKy(JSON.stringify(params), 'hcn.notification', 'getAllNotifications').then(res => {
            if (res.code === 200) {
                this.msgDetail = res.body
                // console.log(this.msgDetail)
            }

        })
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
}
.header .mint-header {
    height: 1rem;
    font-size: .4rem;
    background-color: #35B46F;
}
.session {
    margin-top: 1rem;
    padding-top: .2rem;
}
.session .msgTime {
    width: 3.5rem;
    line-height: .1rem;
    background-color: #e2e2e2;
    color: #fff;
    margin: .2rem auto ;
    font-size: .25rem;
    border-radius: .2rem;
    padding:10px;
    text-align: center;
}
.session .msgList{margin-top: -.2rem;}
.session .msgList li{margin: .3rem .3rem .32rem;}
.session .msgList li .msgContent{
    width: 100%;
    margin-top: .2rem;
    margin-bottom: .2rem;
    background-color: #fff;
    font-size: .28rem;
    color:#666;
    border-radius: 8px;
    padding: .25rem .3rem;
    line-height: .35rem;
    box-sizing:border-box;
    overflow:hidden;
}
.session .msgList li .msgContent h3{
	font-size:0.32rem;
	color:#000;
	margin-bottom:8px;
}
.session .msgList li .msgContent span{
	display:block;
}
.session .msgList li .msgContent b{
	display:block;
	float:right;
	background:url('../../assets/img/ssj_arrow_right.png') no-repeat right center/auto 12px;
	font-weight:normal;
	font-size:.25rem;
	color:#999;
	padding-right:15px;
	margin-top:5px;
}
.session .imgIcon{
    width: .8rem;
    height: .8rem;
}
.session .more{
    font-size: .2rem;
    text-align: center;
    padding-bottom: 10px;
}
</style>
