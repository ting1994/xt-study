<template>
    <div class="app" style="overflow-x:hidden;height:100vh;background-color: #fafafa;">
        <div class="header">
	        <mt-header title="收藏管理">
	            <router-link to="/jia_person" slot="left">
	                <mt-button icon="back"></mt-button>
	            </router-link>
	        </mt-header>
	    </div>
        <div class="session">
        	<mt-navbar v-model="selected">
			    <mt-tab-item id="1">医生</mt-tab-item>
			    <mt-tab-item id="2">医院</mt-tab-item>
			    <mt-tab-item id="3">疾病</mt-tab-item>
			    <mt-tab-item id="4">药品</mt-tab-item>
			    <mt-tab-item id="5">资讯</mt-tab-item>
			    <mt-tab-item id="6">活动</mt-tab-item>
			    <mt-tab-item id="7">讲座</mt-tab-item>
			</mt-navbar>
		    <mt-tab-container v-model="selected">
		      <!--收藏医生-->
			  <mt-tab-container-item id="1">
			  	<div class="all_doctors">
			  		<span class="doctor" v-for="item in collectDoctorList" @click="$router.push('/zy_doctorPage?'+item.doctorId)">
				  		<em></em>
				  		<p>{{item.doctorName}}</p>
				  	</span>
			  	</div>
			  </mt-tab-container-item>
			  <!--收藏医院-->
			  <mt-tab-container-item id="2">
			  	<a class="mint-cell" v-for="item in collectHospitalList" @click="$router.push({path: '/xie_mydoc', query: {orgId: item.orgId}})">
					<span class="mint-cell-mask"></span>
					<div class="mint-cell-left"></div>
					<div class="mint-cell-wrapper">
						<div class="mint-cell-title">
							<span class="mint-cell-text">{{item.shortName}}<b class="hospital_level">{{hospitalLevelName[item.level]}}</b></span>
						</div>
					<div class="mint-cell-value is-link">
						<span></span>
					</div>
					</div>
					<div class="mint-cell-right"></div>
					<i class="mint-cell-allow-right"></i>
				</a>
			  </mt-tab-container-item>
			    <!-- 收藏疾病-->
			  <mt-tab-container-item id="3">
			    <mt-cell v-for="item in collectDiseaseList" :title="item.diseaseEntityName" is-link :to="'//115.236.19.147:14188/ckbserver/view/disease_detail?diseaseEntityId=13853'+item.diseaseEntityId" />
			  </mt-tab-container-item>
			  <!--药品收藏-->
			  <mt-tab-container-item id="4">
			  	<mt-cell v-for="item in collectDrugList" :title="item.medicationName" :label="item.originName" is-link :to="'//115.236.19.147:14188/ckbserver/view/medication_detail?medicationId='+item.medicationId" />
			  </mt-tab-container-item>
			  <mt-tab-container-item id="5">
			  	<ul class="list">
			    	<li v-for="item in collectNewsList" @click="toNewsDetails(item)">
			    		<div class="li_left fl">
			    			<div class="li_left_top">
			    				{{item.title}}
			    			</div>
			    			<div class="li_left_bottom">
			    				<span>{{item.source}}</span>
			    				<span>阅读量<em>{{item.readCount}}</em></span>
			    				<span>{{item.created.split(" ")[0]}} </span>
			    			</div>
			    		</div>
			    		<div class="li_right fl">
			    			<img :src="imgReqUrl + item.listpic"/>
			    		</div>
			    	</li>
			    </ul>
			  </mt-tab-container-item>
			  <mt-tab-container-item id="6">
			  	<ul class="list">
			    	<li v-for="item in collectActivityList" @click="toActivityDetails(item)">
			    		<div class="li_left fl">
			    			<div class="li_left_top">
			    				{{item.title}}
			    			</div>
			    			<div class="li_left_bottom">
			    				<span>{{item.createUser}}</span>
			    				<span>阅读量<em>{{item.readCount}}</em></span>
			    				<span>{{item.createDt.split(" ")[0]}} </span>
			    			</div>
			    		</div>
			    		<div class="li_right fl">
			    			<img :src="imgReqUrl + item.listpic"/>
			    		</div>
			    	</li>
			    </ul>
			  </mt-tab-container-item>
			  <mt-tab-container-item id="7">
			  	<ul class="list">
			    	<li v-for="item in collectLectureList" @click="toActivityDetails(item)">
			    		<div class="li_left fl">
			    			<div class="li_left_top">
			    				{{item.title}}
			    			</div>
			    			<div class="li_left_bottom">
			    				<span>{{item.createUser}}</span>
			    				<span>阅读量<em>{{item.readCount}}</em></span>
			    				<span>{{item.createDt.split(" ")[0]}} </span>
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
        	collectDoctorList:[],
            collectHospitalList:[],
            collectDiseaseList:[],
            collectDrugList:[],
            collectNewsList:[],
            collectActivityList:[],
            collectLectureList:[],
            drugUrl:'http://115.236.19.147:14188/ckbserver/view/medication_detail',
            imgReqUrl: 'http://122.224.131.235:9088/hcn-web/upload/',
            hospitalLevelName: {"0":"全部","10":"一级","11":"一级甲等","12":"一级乙等","13":"一级丙等","20":"二级","21":"二级甲等","22":"二级乙等","23":"二级丙等","30":"三级","31":"三级特等","32":"三级甲等","33":"三级乙等","34":"三级丙等"},
        }
    },
    created() {
        
    },
    methods: {
    	a(obj){return document.getElementById(obj)},
        getCollectDoctorList(){
        	let params = ["f07a053f-17c0-4f19-8d57-4d604fd0f0dd","031",1,20];
	        commonAjax(params, 'hcn.easyDoctor', 'getPatientCollectDetail').then(res => {
                if (res.code === 200) {
                    if (res.body.length) {
                        this.collectDoctorList = res.body
                    } else {
                        this.collectDoctorList = []
                        Toast({
                            message: '暂无结果',
                            duration: 500
                        })
                    }
                }
            })
        },
        getCollectHospitalList(){
        	let params = ["f07a053f-17c0-4f19-8d57-4d604fd0f0dd","021",1,20];
	        commonAjax(params, 'hcn.easyDoctor', 'getPatientCollectDetail').then(res => {
                if (res.code === 200) {
                    if (res.body.length) {
                        this.collectHospitalList = res.body
                    } else {
                        this.collectHospitalList = []
                        Toast({
                            message: '暂无结果',
                            duration: 500
                        })
                    }
                }
            })
        },
        getCollectDiseaseList(){
        	let params = ["0e08eea0d0d948ebaef2bb1483e21648",1,20];
	        commonAjaxKy(JSON.stringify(params), 'hcn.diseaseLibrary', 'queryCollectList').then(res => {
                if (res.code === 200) {
                    if (res.body.length) {
                        this.collectDiseaseList = res.body
                    } else {
                        this.collectDiseaseList = []
                        Toast({
                            message: '暂无结果',
                            duration: 500
                        })
                    }
                }
            })
        },
        getCollectDrugList(){
        	let params = ["0e08eea0d0d948ebaef2bb1483e21648",1,20];
	        commonAjaxKy(JSON.stringify(params), 'hcn.drugLibrary', 'queryCollectList').then(res => {
                if (res.code === 200) {
                    if (res.body.length) {
                        this.collectDrugList = res.body
                    } else {
                        this.collectDrugList = []
                        Toast({
                            message: '暂无结果',
                            duration: 500
                        })
                    }
                }
            })
        },
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
        this.getCollectDoctorList();
        this.getCollectHospitalList();
        this.getCollectDiseaseList();
        this.getCollectDrugList();
        this.getCollectNewsList();
        this.getCollectActivityList();
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
.all_doctors{
	width:100%;
	/*overflow:hidden;*/
	margin:1%;
}
.doctor{
	display:block;
	float:left;
	width:23%;
	background-color:#fff;
	padding:10px 5px 8px;
	margin:1%;
	box-sizing:border-box;
}
.doctor em{
	display:block;
	width:0.8rem;
	height:0.8rem;
	background:url('../../assets/img/zy_doctor.png') no-repeat center center/0.8rem auto;
	border-radius:50%;
	margin:0 auto 6px;
}
.doctor p{
	height:20px;
	line-height:20px;
	font-size:0.26rem;
	text-align:center;
}
.hospital_level{
	margin-left:10px;
	font-weight:normal;
	font-size:0.24rem;
	color:#f39c0e;
}
.list{
	background: #fff;
}
.list li{
	height: 1.3rem;
	width: 100%;
	border-bottom: 0.5px solid #d9d9d9;
}
.li_left{
	width: 70%;
	height: 100%;
	height: 1.3rem;
	color: #000;
	padding: 8px 0.2rem;
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
	display: flex;
	justify-content: space-between;
	height: 100%;
	color: #888;
	height: .6rem;
	font-size: 0.24rem;
	line-height: .6rem;
}

.li_right{
	width: 25%;
	margin: 0.1rem 0 0.1rem 0.1rem;
	display: flex;
	justify-content: flex-end;
}
.li_right img{
	width: 1.1rem;
	height: 1.1rem;
}

</style>
