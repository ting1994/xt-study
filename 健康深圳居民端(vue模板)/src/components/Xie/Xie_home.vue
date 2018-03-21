<template>
	<div class="header_grop" style="background-color:#fff;">
		<!--搜索-->
		<!-- <div class="header_top">
			<div class="search_box">
				<div class="erweima">
					<img class="img_er" src="../../assets/img/erweima1.png">
						<router-link to="/zy_search" class="input_box">
						<img class="img_sear" src="../../assets/img/xie_search.png">
						<input type="text" placeholder="搜索医院、科室、医生、疾病">
						</router-link> -->
						<!-- <img src="../../assets/img/usericon.png" alt=""> -->
						<!-- <span style='font-size:0.1rem;float:right;margin-top:20px;color:#fff;' @click='$router.push("/mybaseinfo2")'>完善</span> -->
				<!-- </div>
			</div>
		</div> -->
		<!--轮播-->
		<div class="box_img" style="height:3.75rem">
			<mt-swipe :auto="5000">
				  <mt-swipe-item><img src="../../assets/img/home_banner1.png" alt="" /></mt-swipe-item>
				  <mt-swipe-item><img src="../../assets/img/home_banner2.png" alt="" /></mt-swipe-item>
				  <mt-swipe-item><img src="../../assets/img/home_banner3.png" @click='$router.push("/downLoadPage")' /></mt-swipe-item>
			</mt-swipe>
		</div>

		<!--mydoctor-->
		<div class="mydoctor">
			<div class="mydoctor_left">
				<div class="doc_jia">
					<span v-if="listobj.name" style="text-align: center;" v-html="listobj.name"></span>
					<span v-else style="text-align: left;">家医签约</span>
					<span v-if="listobj.teamName"  style="text-align: center;">{{listobj.teamName}}</span>
					<span v-else  style="text-align: left;">签约享受健康服务</span>
					<span v-if="listobj.status==2||listobj.status==7||listobj.status==1||listobj.status==6" @click='signNow'>家庭成员签约</span>
					<span v-else="" @click='signNow'>立即签约</span>
				</div>
				<div  class="doc_rig" @click = "ishomepage()">
					<img :src="listobj.avatarFileId?imgReqUrl+listobj.avatarFileId:src" >
					<span v-if="listobj.status==1||listobj.status==6">签约中</span>
					<span v-else style="display: none;"></span>
				</div>
			</div>
				<div class="mydoctor_right" @click="toVisitRecord">

					<div class="jiayi_right left" >
						<h1>就医记录</h1>
						<span class="hei_right left">口袋里的档案夹</span>

					</div>
					<!--<router-link to="/" class="mydoctor_right1_right">-->
					<div class="mydoctor_right1_right">
						<img src="../../assets/img/xie_jyjl.png" />
					</div>
				<!--</router-link>-->

				</div>
			</div>


		<!--点击图标-->
		<div class="box_img1">
			<div class="box_top">
						<div class="box_1">
							<a @click='$router.push("/zy_personal_doctor")'>
							<dt>
								<dl>
									<dt>
										<img src="../../assets/img/xie_srys.png">
									</dt>
									<dd>私人医生</dd>
								</dl>
							</dt>
						</a>
						</div>
					<div class="box_2">
						<a @click='isgy_zjzf()'>
						<dt>
							<dl>
								<dt>
									<img src="../../assets/img/xie_zjzf.png">
								</dt>
								<dd>诊间支付</dd>
							</dl>
						</dt>
					</a>
					</div>
					<div class="box_3">
						<router-link to="/Reportone">
						<dt>
							<dl>
								<dt>
									<img src="../../assets/img/xie_bgcx.png">
								</dt>
								<dd>报告查询</dd>
							</dl>
						</dt>
						</router-link>
					</div>
				</div>
				<div class="box_bottom">
					<div class="box_4">
						<a href="http://115.236.19.147:14188/intelligenceserver/view/index ">
						<dt>
							<dl>
								<dt>
									<img src="../../assets/img/xie_zzzc.png">
								</dt>
								<dd>症状自查</dd>
							</dl>
						</dt>
						</a>
					</div>
					<div class="box_5">
						<!--<router-link to="/">-->
							<a href="http://115.236.19.147:14188/ckbserver/view/index">
						<dt>
							<dl>
								<dt>
									<img src="../../assets/img/xie_jkbk.png">
								</dt>
								<dd>健康百科</dd>
							</dl>
						</dt>
							</a>
						<!--</router-link>-->
					</div>
					<div class="box_6">
						<a @click='noOpen'>
							<dt>
								<dl>
									<dt>
										<img src="../../assets/img/xie_jkjc.png">
									</dt>
									<dd>健康监测</dd>
								</dl>
							</dt>
						</a>
					</div>
				</div>
		</div>

		<!--健康资讯-->
		<!--<div class="jkzx">
			<div class="jkzx_top">
				<div class="span1">
					<img src="../../assets/img/xie_jkzx1.png">
					<span >健康资讯</span>
				</div>
					<router-link to="/jkzx" class="span2">
					<span>查看全部</span>
					<img src="../../assets/img/xie_goright.png">
				</router-link>
			</div>

		  <mt-tab-container-item>
		    <ul class="list">
		    	<li class="li"  v-for="(item, index) in list"  @click="send(item)">
		    		<div class="li_left fl">
		    			<div class="li_left_top">
		    				<span>{{item.title}}</span>
		    			</div>
		    			<div class="li_left_bottom">
		    				<span>{{item.source}}</span>
		    				<span>阅读量<em>{{item.readCount}}</em></span>
		    				<span>{{item.created.split(" ")[0]}} </span>
		    			</div>
		    		</div>
		    		<div class="li_right fl">
		    			<img :src="imgReqUrl + item.listpic" />
		    		</div>
		    	</li>
		    </ul>
		  </mt-tab-container-item>
		</div>-->
		
		
		<div class="jkzx">
		<mt-navbar  v-model="selected">
		  <mt-tab-item id="1">最新</mt-tab-item>
		  <mt-tab-item id="2">高血压</mt-tab-item>
		  <mt-tab-item id="3">糖尿病</mt-tab-item>
		  <mt-tab-item id="4">其他</mt-tab-item>
		</mt-navbar>

		<mt-tab-container v-model="selected">
		  <mt-tab-container-item id="1" >
		    <ul class="list">
		    	<li class="li"  v-for="(item, index) in list"  @click="send(item)">
		    		<div class="li_left fl">
		    			<div class="li_left_top">
		    				{{item.title}}
		    			</div>
		    			<div class="li_left_bottom">
		    				<span>{{item.source}}</span>
		    				<span>阅读量<em>{{item.readCount}}</em></span>
		    				<span>{{time}} </span>
		    			</div>
		    		</div>
		    		<div class="li_right fl">
		    			<img :src="item.listpic"/>
		    		</div>
		    	</li>
		    </ul>
		  </mt-tab-container-item>
		  <mt-tab-container-item id="2">
		     <ul class="list">
		    	<li class="li"  v-for="(item, index) in list"  @click="send(item)" v-if="item.category==1">
		    		<div class="li_left fl">
		    			<div class="li_left_top">
		    				{{item.title}}
		    			</div>
		    			<div class="li_left_bottom">
		    				<span>{{item.source}}</span>
		    				<span>阅读量<em>{{item.readCount}}</em></span>
		    				<span>{{time}}</span>
		    			</div>
		    			<!--<img class="portrait" src="../../assets/img/li_Resident.png"/>-->
		    		</div>
		    		<div class="li_right fl">
		    			<img :src="item.listpic"/>
		    		</div>
		    	</li>
		    </ul>
		  </mt-tab-container-item>
		  <mt-tab-container-item id="3">
		     <ul class="list">
		    	<li class="li"  v-for="(item, index) in list"  @click="send(item)" v-if="item.category==2">
		    		<div class="li_left fl">
		    			<div class="li_left_top">
		    				{{item.title}}
		    			</div>
		    			<div class="li_left_bottom">
		    				<span>{{item.source}}</span>
		    				<span>阅读量<em>{{item.readCount}}</em></span>
		    				<span>{{time}}</span>
		    			</div>
		    		</div>
		    		<div class="li_right fl">
		    			<img :src="item.listpic"/>
		    		</div>
		    	</li>
		    </ul>
		  </mt-tab-container-item>
		  <mt-tab-container-item id="4">
		     <ul class="list">
		    	<li class="li"  v-for="(item, index) in list"  @click="send(item)" v-if="item.category==3">
		    		<div class="li_left fl">
		    			<div class="li_left_top">
		    				{{item.title}}
		    			</div>
		    			<div class="li_left_bottom">
		    				<span>{{item.source}}</span>
		    				<span>阅读量<em>{{item.readCount}}</em></span>
		    				<span>{{time}}</span>
		    			</div>
		    		</div>
		    		<div class="li_right fl">
		    			<img :src="item.listpic"/>
		    		</div>
		    	</li>
		    </ul>
		  </mt-tab-container-item>
		</mt-tab-container>
	</div>

		<!--底部按钮-->
		<div class="flexbox">
				<router-link to="/xie_home" class="flex_left" >
						<div class="xie_img_box">
							<img src="../../assets/img/xie_shouye1.png">
						</div>
						<span>首页</span>
				</router-link>
				<router-link to="/xie_xiaoxi" class="flex_center">
						<div class="xie_img_box">
							<img src="../../assets/img/xie_mess.png" >
							<b v-show="con>0">{{con}}</b>
						</div>
						<span>消息</span>
				</router-link>
				<router-link to="/zy_service" class="flex_right">
						<div class="xie_img_box">
							<img src="../../assets/img/xie_fuwu.png" >
						</div>
						<span>服务</span>
				</router-link>
				<router-link to="/jia_person" class="flex_right1">
						<div class="xie_img_box">
							<img src="../../assets/img/xie_my.png" >
						</div>
						<span>我的</span>
				</router-link>
			</div>
			<!--<mt-tabbar class="xie_selected">
			  <mt-tab-item @click.native='$router.push("/xie_home")'>
			    <img slot="icon" src="../../assets/img/xie_shouye1.png">首 页

			  </mt-tab-item>
			  <mt-tab-item @click.native="$router.push('/xie_xiaoxi')">
			    <img slot="icon" src="../../assets/img/xie_my.png">
			    消 息
			  </mt-tab-item>
			  <mt-tab-item @click.native='$router.push("/zy_service")'>
			    <img slot="icon" src="../../assets/img/xie_my.png">
			    服 务
			  </mt-tab-item>
			  <mt-tab-item @click.native='$router.push("/jia_person")'>
			    <img slot="icon" src="../../assets/img/xie_my.png">
			    我 的
			  </mt-tab-item>
			</mt-tabbar>-->

	</div>
</template>

<script>var md5 = require("md5");
import { Indicator, Toast, MessageBox } from 'mint-ui'
import { commonAjax,imgUrl } from '../../api/api'
import { commonAjaxKy } from '../../api/api'
import { GoMyhApp } from '../../assets/js/txb_lifesea.wx.jssdk.js'
import { mapState } from 'vuex'
import '../../assets/css/li_style.css'
var imgUrlid=require("../../assets/img/li_Resident.png")
export default {
	compoents: {

	},
	data() {
		return {
			list: [],
			selected: '1',
            imgurlm:imgUrlid,
            time: '',
			serverUrl: 'fzx.lifesea.com:8099', //生命海赋值
			// openId:sessionStorage.getItem('userInfo').certificate.certificateNo,//患者信息唯一标识
			openId: '',
			appKey: '8jczFSmHiXKcZEjf', //生命海赋值
			cryptkey: '190ee8a2f6d44fc4', //生命海赋值
			xie_common: {},
			imgReqUrl: 'http://122.224.131.235:9088/hcn-web/upload/',
			flag: '',
			firstLogin: false,
			con: '',
			listobj:{},
			src:require('../../assets/img/xie_doctor.png')
		}
	},
	computed: {

	},
	methods: {
		//健康信息的推送
		getAppInfoByDevice() {
			let params = []
			commonAjaxKy(JSON.stringify(params), 'hcn.device', 'getAppInfoByDevice').then(res => {
				if(res.code == 200) {
//					console.log(res.body.hasOwnProperty('user'))
					if(res.body.hasOwnProperty('user')) {
						this.firstLogin = false
						this.openId = res.body.user.certificate.certificateNo
					this.$store.dispatch('xie_common', { "certificateNo": res.body.user.certificate.certificateNo, "userName": res.body.userName })
					sessionStorage.setItem('phoneNo', res.body.user.phoneNo)
					sessionStorage.setItem('userInfoDetail', JSON.stringify(res.body.user))
					} else {
						this.firstLogin = true
					}
				}
			})
		},
		noOpen() {
			Toast({
				message: '暂未开通',
				duration: 1000
			})
		},
		getAllNotificationCount() {
			let params = []
			let me = this
			commonAjaxKy(JSON.stringify(params), 'hcn.notification', 'getAllNotificationCount').then(res => {
				if(res.code == 200) {
					//					this.$store.dispatch('xie_common',{"body":res.body})
					let count = 0
					res.body.forEach(item => {
						count += item.count
						me.con = count
					})
				}
			})
		},
		getUpList() {
			Indicator.open('加载中...');
                let params = []
                commonAjax(params, 'pcn.pcnHealthNewsService', 'getUpList').then(res => {
                    if (res.code == 200) {
                    	console.log(res)
                    	console.log(res.body.list)
	                  	this.list = res.body.list
	                 
	                  	 for(var i=0;i<res.body.list.length;i++){
	                  	 	//时间转换
	                  	 	this.time = res.body.list[i].created.split(" ")[0]
	                        //头像选择拼接
	                        if(res.body.list[i].listpic==0){
	                            res.body.list[i].listpic=this.imgurlm
	                        }else{
	                            res.body.list[i].listpic=imgUrl(res.body.list[i].listpic)
	                        }

                        }

	                  	Indicator.close();
                    }
                })
		},
		querySignApplyInfo() {
			let params = ["hcn.shenzhen", JSON.parse(sessionStorage.getItem("userInfo")).body.userId]
			// console.log(params);
			let me = this
			commonAjax(JSON.stringify(params), 'pcn.residentSignService', 'querySignApplyInfo').then(res => {
				if(res.code == 200) {
					console.log(res.hasOwnProperty('body')===false)
					if(res.hasOwnProperty('body')===false){
						me.listobj.status =15
//						me.listobj.avatarFileId=0
						console.log(me.listobj.avatarFileId)
//						me.listobj.teamName=""
//						me.listobj.name="1"
					}else{
						this.listobj = res.body;
						sessionStorage.setItem('common_signApplyInfo', JSON.stringify(res.body));
					}
//					sessionStorage.setItem('common_signApplyInfo', JSON.stringify(res.body));
				}
			})
		},
		send(item) {
			//点击到跳转到咨讯详情
			this.$store.dispatch('xie_common', { "id": item.id })
			this.$router.push("/jkzx_detail")
		},
		//      	跳转生命还就医记录
		toVisitRecord() {
			// alert("患者信息唯一标识" + this.openId);
			GoMyhApp({ "serverUrl": this.serverUrl, openId: this.openId, appKey: this.appKey, cryptkey: this.cryptkey });
		},
		//判断是否第一次登陆
		signNow() {
			if(this.firstLogin) {
				MessageBox({
					title: '提示',
					message: '请先完善个人信息'
				}).then(() => {
					this.$router.push("/mybaseinfo2")
				})
			} else {
				this.$router.push("/zbl_jmqy")
			}
		},
		ishomepage() {
			if(this.firstLogin) {
				MessageBox({
					title: '提示',
					message: '请先完善个人信息'
				}).then(() => {
					this.$router.push("/mybaseinfo2")
				})
			} else {
				this.$router.push("/qyxq_signed")
			}
		},
		isgy_zjzf() {
			if(this.firstLogin) {
				MessageBox({
					title: '提示',
					message: '请先完善个人信息'
				}).then(() => {
					this.$router.push("/mybaseinfo2")
				})
			} else {
				this.$router.push("/gy_zjzf")
			}
		}
	},

	created() {
		this.querySignApplyInfo()
	},
	mounted(){
		this.getAppInfoByDevice()
		this.getAllNotificationCount()
		this.getUpList()
	}

}</script>

<style lang='stylus' scoped>
@import "../../assets/css/xie_style.css"

	.left{
		float: left;
	}
	.right{
		float: right;
	}
	/*.header_grop{
		width: 100%;
		height: 100%;
	}*/
	.header_top{
		width: 100%;
		height: 1rem;
		 background: linear-gradient(to right, #2FB86D, #68CC70)
	}
	.erweima .img_er{
		height: .4rem;
		width: 0.4rem;
		margin-top: 0.3rem;
		margin-left: .3rem;
		float: left;

	}
	.input_box{
		height: .7rem;
		float: left;
		width: 6rem;
		margin-left: .3rem;
		margin-top: .15rem;
		border-radius: .1rem;
		background: #fff;
	}
	.img_sear{
		height: .4rem;
		width: 0.4rem;
		margin-top: 0.2rem;
		margin-left: .6rem;
		float: left;
	}
	.input_box input{
		width: 4rem;
		height: .6rem;
		line-height: .6rem;
		border: none;
		outline: none;
		float: left;
		padding-top: .1rem;
		font-size: .3rem;
	}

	.box_img img{
		height: 3.75rem;
		width: 100%;
	}
	.box_img{
	height: 2.5rem;
	}


	.mydoctor{
		height: 1.7rem;
		margin-top: .2rem;
		margin-bottom: .2rem;
		display: flex;
		/*border: 1px solid red;*/
	}
	.mydoctor_left,.mydoctor_right{
		flex: 1 1 40%;
		/*border: 1px solid red;*/
		margin-left: .2rem;

	}
	.mydoctor_right{
		margin-right: .2rem;
	}
	.mydoctor_left{
		 background: #fdfcef
	}
	.mydoctor_left,.mydoctor_right{
		width: 3.44rem;
	}

	.mydoctor_right{
		position: relative;
		background: #F4FEFE;
		display: flex;
		flex-direction: column;
		text-align: center;
	}
	.jiayi_right h1{
		text-align: left;
		width: 2rem;
		color:#333;
		margin-left: .2rem;
		font-size: .32rem;
		/*font-weight: 600;*/
		margin-top: .46rem;

	}
	.jiayi_right{
		height: 1.7rem;
	}
	/*.hei_right{
		font-size: 0.2rem;
		margin-top: .2rem;
		color: #999;
		width: 2rem;
		overflow:hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}*/
	.doc_jia{
		display: flex;
		flex-direction: column;
		align-content: center;
		text-align: center;
		padding: 0 0 0 .16rem;
	}
	.doc_jia>span:first-child{
		margin-top: .2rem;
		width: 2rem;
		font-size:.32rem;
		/*font-weight: bold;*/
		color: #323232;
	}
	.doc_jia>span:nth-child(2){
		width: 2rem;
		font-size: .2rem;
		margin-top: .1rem;
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
		color: #999;
	}
	.doc_jia span:nth-child(3){

		width: 2rem;
		padding: .1rem 0rem;
	    border: 1px solid #2FB86D;
	    color: #67cc70;
	    font-size: .2rem;
	    border-radius: .1rem;
	    margin-top: .1rem;
	}
	.doc_rig{
		position: relative;
	}
	.doc_rig span{
		position:absolute;
		top: -.4rem;
		right: 0.2rem;
		padding: .05rem .05rem;
		color: #fff;
		font-size: .16rem;
		border-radius: .1rem;
		background: #FFB90F;
	}
	.doc_rig img{
	width: 1.14rem;
    height: 1.14rem;
    border-radius:50%;
    position: absolute;
    top: -1.2rem;
    right: .1rem;
	}
	.mydoctor_right1_right img{
	width: 1.14rem;
    height: 1.14rem;
    position: absolute;
    top: .2rem;
    right: .1rem;
    border-radius: 50%;

	}
	.hei_right{
		font-size: 0.2rem;
		margin-top: .2rem;
		color: #999;
		width: 2rem;
		overflow:hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
		margin-left: .15rem;
		text-align: left;
	}
	/*
	.mydoctor_right1{
		position: relative;
	}

	.mydoctor_right1 img{
	width: 1.2rem;
    height: 1.2rem;
    border-radius:50%;
    position: absolute;
    top: -.8rem;
    right: .1rem;
	}*/
	.box_top,.box_bottom,.box_bottom1{
	flex: 1 1 33%;
	display: flex;
}
.box_1,.box_2,.box_3,.box_4,.box_5,.box_6{
	flex: 1 1 33%;
}

.header_grop dt img{
	width: 1.2rem;
	height: 1.2rem;
	padding-top:0.3rem
}
dd{
	font-size: 0.28rem;
	color: #666;
	/*margin-bottom: .2rem;*/
	margin-top: .2rem;
}
dt{
	text-align: center;
}
.box_img1{
	margin-bottom: .3rem;
}
/*健康资讯*/
.jkzx{
	/*height: 5rem;*/
}

/*底部*/
.flexbox{
	border-top: 1px solid #ccc;
	height: 1rem;
	position: fixed;
	bottom: 0;
	width: 100%;
	display: flex;
	background: #fff;
}
.flex_left,.flex_center,.flex_right,.flex_right1{
	flex: 1 1 25%;
	display: flex;
	flex-direction:column;
}
.xie_img_box{
	height: 0.5rem;
}
.xie_img_box b{
	font-size: .2rem;
    width: .3rem;
    height: .3rem;
    line-height: .3rem;
    border-radius: 50%;
    color: #FFFFff;
    float: left;
    background: red;
    position: absolute;
    right: 4.4rem;
    top: 0.1rem;
    text-align: center;
}
.flexbox img{
	width: 0.4rem;
    height: 0.4rem;
    margin: 0 auto;
    display: block;
    padding-top: .1rem;

}
.flexbox span{
	font-size: 0.22rem;
	text-align: center;
	height: 0.5rem;
	padding-top: 0.1rem;
}


.jkzx_top{
	height: .8rem;
	border-bottom: 1px solid #ccc;
	display: flex;
	 justify-content:space-between;
	 align-items: center;
}
.jkzx_top .span1{
	/*height: .8rem;*/
	color: #323232;
	font-size: .32rem;
	display: flex;
	align-items: center;
}
.jkzx_top .span2{
	/*height: .8rem;*/
	font-size: .24rem;
	display: flex;
	align-items: center;
	color: #999;
}
.span1 img{
	width: .4rem;
	height: .4rem;
	/*padding-top: .2rem;*/
	margin: 0 .2rem 0 .2rem;
}

.span2 img{
	width: .5rem;
	height: .5rem;
/*	margin-top: .2rem;*/
}
 a:hover{color: #333333}
 a:link {color: #333333}
 a:visited{color: #333333}

 .jkzx .mint-header{
		height: 1rem;
		background-color: #35B46F;
		color: #26a2ff;
	}
.jkzx .mint-header-button{
	display: block;
	flex: 0;
}
.jkzx .mint-button{
		height: 1.5rem;
}
.jkzx .mintui-back{
		font-size: 0.37rem;
		background: #fff;
	}
.jkzx .mint-button-icon{
		color: #fff;
	}
.jkzx .is-right{
	display: flex;
	 direction: rtl;
}
.jkzx .mint-navbar{
	margin-top: 1rem;
	height: 1rem;
	line-height: 1rem;
}

.mint-tab-item-label{
	font-size: 0.28rem;
}
.mint-tab-item{
	display: flex;
	align-items: center;
	justify-content: center;
}
.mint-navbar{
	margin-top: 1rem;
	height: 1rem;
}
.mint-tab-container-wrap{
	margin-top: 2rem;
}
.mint-navbar{
	border-bottom: 0.5px solid #ccc;
	border-top: 0.5px solid #ccc;
}
.mint-cell-left{
	margin-left: 0.5rem;
}
.list{
	background: #fff;
}
li{
	height: 1.2rem;
	width: 100%;
	border-bottom: 0.5px solid #ccc;
}
.li_left{
	width: 65%;
	height: 100%;
	font-size: 0.22rem;
	height: 1.2rem;
	color: #000;
	padding: 0 0.2rem;
}
.li_left_top{
	display: flex;
	justify-content: flex-start;
	align-items: center;
	font-size: 0.28rem;
	height: .6rem;
	overflow: hidden; /*自动隐藏文字*/
    text-overflow: ellipsis;/*文字隐藏后添加省略号*/
    white-space: nowrap;/*强制不换行*/
    width: 20em;/*不允许出现半汉字截断*/
   color: #323232;
}
.li_left_top span{
	overflow: hidden; /*自动隐藏文字*/
    text-overflow: ellipsis;/*文字隐藏后添加省略号*/
    white-space: nowrap;/*强制不换行*/
    width: 5rem;/*不允许出现半汉字截断*/
}
.li_left_bottom{
	display: flex;
	justify-content: space-between;
	height: 100%;
	color: #999;
	height: .6rem;
	line-height: .6rem;
}

.li_right{
	width: 25%;
	margin: 0.1rem 0 0.1rem 0.1rem;
	display: flex;
	justify-content: flex-end;
}
.li_right img{
	width: 1rem;
	height: 1rem;
	border-radius: 2px;
}
.mint-tab-container-item{
	margin-bottom: 1rem;
}
#yanse{
background: linear-gradient(to right, #2FB86D, #68CC70)}

/*插件*/
/*.xie_selected{
	position:fixed;
}
.xie_selected img{
	width: .5rem;
	height:.5rem
}
.xie_selected .mint-tab-item{
	display: flex;
	flex-direction:column;
}
.xie_selected .mint-tab-item-icon,.xie_selected .mint-tab-item-label{
	flex: 1 1 50%;
}*/
</style>
