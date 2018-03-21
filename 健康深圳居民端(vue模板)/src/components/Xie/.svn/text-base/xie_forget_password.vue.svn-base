<template>
	<div class="header-grop">
		<mt-header title="忘记密码" style="background: #FFFFFF;font-size: 0.3rem;color: #000000;">
			  <router-link to="/xie_homepage" slot="left">
			    <mt-button icon="back"></mt-button>
			  </router-link>
		</mt-header>
		<div class="img_phone">
			<div>
				<img src="../../assets/img/xie_forgetphone.png" >
			</div>
			<span>请输入手机号</span>
			<input type="text" placeholder="请输入手机号" v-model="phone">
			<div class="buttom_box">
				<mt-button size="large" @click.native="succ" style="background:#5EC671;color: #fff;font-size: .32rem;">获取验证码</mt-button>
			</div>
		</div>
	</div>
</template>
<script>
import { getValidation }from '../../api/api';
import { MessageBox } from 'mint-ui';
export default {
	components: {

	},
	data() {
		return {
			phone:''
		}

	},
	computed: {

	},
	methods: {
		//获取验证码
		succ () {
			if (/^1[34578]\d{9}$/.test(this.phone)) {
					this.getPassword()
			} else {
				MessageBox('提示', '手机号输入错误');
			}
		},

		//获取验证码
		getPassword () {
			let params=["hcn.shenzhen","patient",this.phone,"pwd"]
			console.log(params)
			getValidation(JSON.stringify(params), 'hcn.smsService', 'getIdentifyingCode').then(res => {
				if(res.code == 200) {
					  sessionStorage.setItem("xie_username",this.phone);
					  this.$router.push('/xie_verification')
				} else if(res.code == 606){
					MessageBox('提示', res.msg);
				}else{
					MessageBox('提示',"当前用户未注册")
				}
			})

		},
	},
	mounted () {},
}</script>
<style lang="less" scoped>.header-grop {
	.img_phone {
		margin-top: 1rem;
		display: flex;
		flex-direction: column;
		/*justify-content:center;
		align-content: center;*/
		text-align: center;
		div:first-child {
			/*text-align: center;*/
			img {
				width: 2rem;
				height: 2rem;
			}
		}
		span {
			margin-top: .6rem;
			font-size: .28rem;
			color: #35b46f;
		}
		input {
			margin: 0 auto;
			text-align: center;
			margin-top: .4rem;
			font-size: .32rem;
			color: #999;
			border: none;
			outline: none;
			width: 80%;
			padding: 0 0 .4rem 0;
			border-bottom: 1px solid #999;
		}
		.buttom_box {
			margin: 0 auto;
			margin-top: .6rem;
			width: 80%;
			height: .88rem;
		}
	}
}</style>
