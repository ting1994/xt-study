<template>
<div class="header_group">
	<!--头部注册-->
	<div class="header_top">
		<img @click='$router.push("/xie_homepage")' class="header_icon" src="../../assets/img/xie_go_1.png">
		<div class="header_center">
			<div class="header_img">
				<img src="../../assets/img/1024.png" />
			</div>
			<span>注册</span>
		</div>
		<div></div>
	</div>
	<!--中间form-->
	<div class="Nosubmint">
		<mt-field label="手机号" placeholder="请输入您的手机号" type="tel" v-model="phone"></mt-field>
		<mt-field label="验证码" v-model="captcha" placeholder="请输入您的验证码">
			<b v-show="!isshow" @click="getcaptcha()">获取验证码</b>
			<b v-show="isshow">{{time}}s</b>
		</mt-field>
		<mt-field label="密码" placeholder="6-20位数字、字母或字符" type="password" v-model="password" id="pwd">
			<!--mint-field-core-->
			<div @click="valp" class="home_delete" v-show="isshow3" >
						<img src="../../assets/img/xie_express.png">
					</div>
					<div @click="valp" class="home_delete" v-show="!isshow3">
						<img  src="../../assets/img/xie_the_dark.png" >
					</div>
		</mt-field>
					
	</div>
	<div class="buttom_box">
		<mt-button size="large" @click="succ" style="background:#5EC671;color: #fff;">注 册</mt-button>
	</div>
</div>
</template>

<script>
var md5 = require("md5");
import {
	commonAjax,
	commonAjaxKy,
	residentRegister
} from '../../api/api';
import {
	MessageBox
} from 'mint-ui';
export default {
	components: {

	},
	data() {
		return {
			isshow3:false,
			phone: '',
			errshow: false,
			yanzm: '',
			phones: '',
			isshow: '',
			time: 60,
			captcha: '',
			password: '',
			isshow1: '',
		}

	},
	computed: {

	},
	methods: {
		//		明文暗问
		valp(){
			console.log(document.querySelector("#pwd input").value)
			if(this.isshow3==false){
				this.isshow3=true
				document.querySelector("#pwd input").type='text'
			}else{
				this.isshow3=false
				document.querySelector("#pwd input").type='password'
			}
		},
		getcaptcha() {
			//验证手机格式是否正确
			if (/^1[34578]\d{9}$/.test(this.phone)) {
				this.getyanzm()
			} else {
				MessageBox('提示', '手机号输入错误');

			}
		},
		getyanzm() {
			this.getIdentifyingCode()
			this.isshow = !this.isshowl
			let timeOut = setInterval(() => {
				let that = this
				if (that.time === 0) {
					clearInterval(timeOut);
					that.isshow = !that.isshow;
					that.time = 60;
				}
				this.time--
			}, 1000)
		},
		//		获取验证码
		getIdentifyingCode() {
			let params = ["hcn.shenzhen", "patient", this.phone, "register"]
			residentRegister(JSON.stringify(params), 'hcn.smsService', 'getIdentifyingCode').then(res => {
				console.log(res);
				if (res.code == 200) {
					//  console.log(res.body)
				} else if (res.code == 603) {
					MessageBox('提示', '当前用户已注册');
				} else if (res.code == 606) {
					MessageBox('提示', '1分钟内不允许重新获得验证码');
				}
			})

		},
		//      设置密码

		registerPatientWithInviteCode() {
			let params = ["hcn.shenzhen", this.phone, md5(this.password), this.captcha, ""]
			residentRegister(JSON.stringify(params), 'hcn.register', 'registerPatientWithInviteCode').then(res => {
				if (res.code == 200) {
					MessageBox('提示', '注册成功');
					this.$router.push('/xie_homepage')
				} else {
					MessageBox('提示', res.msg);
				}
			})
		},
		//点击注册
		succ() {
			if (/^[\w.]{6,20}$/.test(this.password)) {
				this.registerPatientWithInviteCode()
			} else {
				MessageBox('提示', "密码由6-20位数字英文字母组成")
			}

		},
		changge() {
			if (this.isshow1 == false) {
				this.isshow1 = true
				this.$refs.changeimg.type = "text"

			} else {
				this.isshow1 = false
				this.$refs.changeimg.type = "password"
			}

		},

	},

	mounted() {

	},

}
</script>

<style scoped>
	@import url("../../assets/css/xie_style.css");
.header_group {
	/*text-align: center;*/
	position: absolute;
	left: 0;
	right:0;
	top:0;
	bottom:0;
	background: #f2f2f2;
}

.header_top {
	height: 3.4rem;
    display: flex;
    justify-content: space-between;
    background: #5EC671;
    padding: .3rem;
}

.header_top>img {
	width: .3rem;
	height: .3rem;
	float: left;
}

/*.header_icon {
	height: .8rem;
	width: .8rem;
	float: left;
}*/

.header_center img {
	height: 1.8rem;
	width: 1.8rem;
}

.header_center {
	font-size: .3rem;
	display: flex;
	flex-direction:column;
	justify-content: center;
	/*height: 2rem;
	width: 2rem;*/
}

.header_center span {
	font-size: .36rem;
    margin-top: .3rem;
    color: #fff;
    text-align: center;
}

.header_img {
}


/*验证码*/

.mint-field-other b {
	color: #fff;
	background: #F1C50E;
	padding: .1rem .2rem;
	border-radius: .1rem;
	font-size: .28rem;
	font-weight: 100;
}

/*.Nosubmint {
	margin-top: 0.3rem;
}*/
.Nosubmint .mint-cell-wrapper {
	padding: 0 .3rem;
}
.buttom_box{
	text-align: center;
	width: 6rem;
	height: .88rem;
	
	margin: 0 auto;
	margin-top: .6rem;
	/*background: #5EC671;*/
}
#pwd img{
	width: .7rem;
	height: .7rem;
}
</style>
