<template>
    <div class="app" style="overflow-x:hidden;height:100vh;background-color: #f2f2f2;">
        <div class="header">
	        <mt-header title="健康资讯">
	            <router-link to="" slot="left">
	                <mt-button icon="back"></mt-button>
	            </router-link>
	        </mt-header>
	    </div>
        <div class="session">
        	<mt-navbar v-model="selected">
			    <mt-tab-item id="1">最新</mt-tab-item>
			    <mt-tab-item id="2">糖尿病</mt-tab-item>
			    <mt-tab-item id="3">高血压</mt-tab-item>
			    <mt-tab-item id="4">其他</mt-tab-item>
			</mt-navbar>
		    <mt-tab-container v-model="selected">
			  <!--本人相关-->
			  <mt-tab-container-item id="1">
			  	<ul class="list">
			    	<li>
			    		<div class="li_left fl">
			    			<h3 class="li_left_top">
			    				举办“关爱少儿安全健康”首场活动
			    			</h3>
			    			<div class="li_left_bottom">
			    				<span>高血压&nbsp;老年人&nbsp;孕产妇</span>
			    				<span>
			    					<em class="doctor">张庆伟 副主任医师</em>
			    					<em class="time">2017.01.12</em>
			    				</span>
			    			</div>
			    		</div>
			    		<div class="li_right fl">
			    			<!--<img :src="imgReqUrl + item.listpic"/>-->
			    		</div>
			    	</li>
			    </ul>
			  </mt-tab-container-item>
			    <!-- 全部宣教-->
			  <mt-tab-container-item id="2">
			  	<ul class="list">
			    	<li v-for="item in collectNewsList" @click="">
			    		<div class="li_left fl">
			    			<h3 class="li_left_top">
			    				{{item.title}}
			    			</h3>
			    			<div class="li_left_bottom">
			    				<span>高血压&nbsp;老年人&nbsp;孕产妇</span>
			    				<span>
			    					<em class="doctor">张庆伟 副主任医师</em>
			    					<em class="time">2017.01.12</em>
			    				</span>
			    			</div>
			    		</div>
			    		<div class="li_right fl">
			    			<img :src="imgReqUrl + item.listpic"/>
			    		</div>
			    	</li>
			    </ul>
			  </mt-tab-container-item>
			</mt-tab-container>
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
import { MessageBox,Toast,Badge,Cell,Navbar,TabItem,Tabbar,TabContainer, TabContainerItem  } from 'mint-ui'
export default {
    data: function() {
        return {
        	selected:'1',
            collectNewsList:[],
            drugUrl:'http://115.236.19.147:14188/ckbserver/view/medication_detail',
            imgReqUrl: 'http://122.224.131.235:9088/hcn-web/upload/',
            hospitalLevelName: {"0":"全部","10":"一级","11":"一级甲等","12":"一级乙等","13":"一级丙等","20":"二级","21":"二级甲等","22":"二级乙等","23":"二级丙等","30":"三级","31":"三级特等","32":"三级甲等","33":"三级乙等","34":"三级丙等"},
        }
    },
    created() {
        
    },
    methods: {
    	a(obj){return document.getElementById(obj)},
        getCollectNewsList(){
        	let params = [{"pageSize":20,"pageNo":1}];
	        commonAjax(params, 'pcn.pcnHealthNewsService', 'getUserMarkInfo').then(res => {
                if (res.code === 200) {
                    if (res.body.list.length) {
                        this.collectNewsList = res.body.list
                    } else {
                        this.collectNewsList = []
                        Toast({
                            message: '暂无结果',
                            duration: 500
                        })
                    }
                }
            })
        },
        toNewsDetails(item){
        	//点击到跳转到咨讯详情
        	this.$store.dispatch('xie_common',{"id":item.id})
        	this.$router.push("/jkzx_detail")
        },
        toActivityDetails(item){
        	//点击到跳转到活动/讲座详情
			this.$store.dispatch('xie_common',{"id":item.id})
        	this.$router.push("/zy_event_detail")
        },
    	getCollectActivityList(){
        	let params = [{"pageSize":20,"atype":1,"pageNo":1}];
	        commonAjax(params, 'pcn.pcnHealthActivitiesService', 'getUserMarkInfo').then(res => {
                if (res.code === 200) {
                    if (res.body.list.length) {
                        this.collectActivityList = res.body.list
                    } else {
                        this.collectActivityList = []
                        Toast({
                            message: '暂无结果',
                            duration: 500
                        })
                    }
                }
            })
        },
        getCollectLectureList(){
        	let params = [{"pageSize":20,"atype":2,"pageNo":1}];
	        commonAjax(params, 'pcn.pcnHealthActivitiesService', 'getUserMarkInfo').then(res => {
                if (res.code === 200) {
                    if (res.body.list.length) {
                        this.collectLectureList = res.body.list
                    } else {
                        this.collectLectureList = []
                        Toast({
                            message: '暂无结果',
                            duration: 500
                        })
                    }
                }
            })
        }
        
    },
    mounted() {
        this.getCollectNewsList();
    },
    destroyed() {
    	
    }
}
</script>

<style lang='stylus' scoped>
mainColor = #4eab52
greyFont = #ADADAD
fontSize = .4rem
.header {
    position: fixed;
    z-index: 999;
    top: 0;
    left: 0;
    right: 0;
    .mint-header {
        height: 1rem;
        font-size: fontSize;
        color: #fff;
        background-color: #3AB76F;
    }
}
.session {
    margin-top: 1rem;
    margin-bottom: 1rem;
} 
.session .mint-navbar{
	border-bottom:1px solid #d9d9d9;
}
.session .mint-cell{
	margin-top:-1px;
}
.mint-navbar .mint-tab-item.is-selected{
	color:#35b46f;
	border-bottom:3px solid #35b46f;
	margin-bottom:0;
}
.list{
	background: #fff;
}
.list li{
	height: 1.56rem;
	width: 100%;
	border-bottom: 0.5px solid #d9d9d9;
}
.li_left{
	width: 70%;
	height: 100%;
	height: 1.56rem;
	color: #000;
	padding: 10px 0.2rem;
	box-sizing:border-box;
}
.li_left_top{
	/*display: flex;
	justify-content: flex-start;
	align-items: center;*/
	font-size: 0.28rem;
	height: .6rem;
	line-height:.3rem;
	display: -webkit-box;
	overflow: hidden;
    text-overflow: ellipsis;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
	/*margin-bottom:10px;*/
}
.li_left_bottom{
	height: 100%;
	color: #888;
	height: .8rem;
	font-size: 0.24rem;
	line-height: .3rem;
}
.li_left_bottom span{ 
	display:block;
}
.li_left_bottom span em{
	padding-left:15px;
}
.li_left_bottom span .doctor{
	background:url('../../assets/img/ssj_icon_person.png') no-repeat left center/auto 12px;
	margin-right:15px;
}
.li_left_bottom span .time{
	background:url('../../assets/img/ssj_icon_time.png') no-repeat left center/auto 12px;
}
.li_right{
	width: 25%;
	margin: 0.2rem 0 0.2rem 0.1rem;
	border-radius:8px;
	overflow:hidden;
}
.li_right img{
	display:block;
	width: 1.8rem;
	height: 1.18rem;
}

</style>
