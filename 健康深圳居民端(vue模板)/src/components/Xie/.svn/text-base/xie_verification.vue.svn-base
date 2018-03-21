<template>
	<div class="header-grop">
		<mt-header title="忘记密码" style="background: #FFFFFF;font-size: 0.3rem;color: #000000;">
			<router-link to="/xie_forget_password" slot="left">
				<mt-button icon="back"></mt-button>
			</router-link>
		</mt-header>
		<div class="img_phone">
			<div>
				<img src="../../assets/img/xie_yanzm1.png">
			</div>
			<span>请输入{{phone|numbe}}手机收到的验证短信</span>
			<!--<input type="number" placeholder="请输入验证码">-->
			<div id="AccountNumber">
				<input maxlength="1" v-model="input1" type="tel">
				<input maxlength="1" v-model="input2" type="tel">
				<input maxlength="1" v-model="input3" type="tel">
				<input maxlength="1" v-model="input4" type="tel">
				<input maxlength="1" v-model="input5" type="tel">
				<input maxlength="1" v-model="input6" type="tel">
				<span v-show="ishow" @click="dianji">重新发送</span>
				<span v-show="!ishow">{{time}}</span>
			</div>

		</div>
		<div class="buttom_box" @click="next">
			<mt-button size="large" style="background:#5EC671;color: #fff;font-size: .32rem;">下一步</mt-button>
		</div>
	</div>
</template>
<script>
	import { commonAjax, getValidation }
	from '../../api/api';
	import { MessageBox } from 'mint-ui';
	export default {

		components: {

		},
		data() {
			return {
				phone: sessionStorage.getItem("xie_username"),
				time: 60,
				ishow: false,
				input1: '',
				input2: '',
				input3: '',
				input4: '',
				input5: '',
				input6: '',
			}

		},
		computed: {

		},
		methods: {
			dianji() {
				let params=["hcn.shenzhen","patient",sessionStorage.getItem("xie_username"),"pwd"]
				getValidation(JSON.stringify(params), 'hcn.smsService', 'getIdentifyingCode').then(res => {
				if(res.code == 200) {
				}
			})
				this.ishow = !this.ishow
				this.yanzm()
			},
			yanzm() {
				let timeOut = setInterval(() => {
					let that = this
					if(that.time === 0) {
						clearInterval(timeOut);
						that.ishow = !that.ishow;
						that.time = 60;
					}
					this.time--
				}, 1000)
			},
			//			onloadd() {
			//				let txts = document.getElementById("AccountNumber").getElementsByTagName("input");
			//				for(let i = 0; i < txts.length; i++) {
			//					let t = txts[i];
			//					t.index = i;
			//					t.setAttribute("readonly", true);
			//					t.onkeyup = function(event) {
			//						let me = this
			//						let last = event.timeStamp
			//						setTimeout(function() {
			//							if(last - event.timeStamp == 0) {
			//								if(event.keyCode == 8) {
			//									me.value = "";
			//									let behand = me.index - 1;
			//									if(behand < 0) return;
			//									txts[behand].removeAttribute("readonly");
			//									txts[behand].focus();
			//								} else {
			//									me.value = me.value.replace(/^(.).*$/, '$1');
			//									let next = me.index + 1;
			//									if(next > txts.length - 1) return;
			//									txts[next].focus();
			//								}
			//							}
			//						}, 10)
			//					}
			//				}
			//			},
						onloadd() {
							let btn = document.getElementById("AccountNumber")
							let input = btn.children
							btn.addEventListener('keyup', function(event) {
								let last = event.timeStamp
								setTimeout(function() {
									if(last - event.timeStamp == 0) {
										if(event.keyCode == 8) {
											if(event.target.previousSibling.previousSibling != null) {
//												event.target.value = ""
												event.target.previousSibling.previousSibling.focus()
											} else return;
										} else {
											if(event.target.nextSibling.nextSibling != null) {
												event.target.blur()
												event.target.nextSibling.nextSibling.focus()
											} else return;
										}
									}
								}, 10)
			
							})
						},
			Passwordvalid() {
				let yzm = this.input1 + this.input2 + this.input3 + this.input4 + this.input5 + this.input6
				console.log(yzm)
				let params = [sessionStorage.getItem('xie_username'), yzm]
				getValidation(JSON.stringify(params), 'hcn.smsService', 'validateCode').then(res => {
					if(res.code == 200) {
						this.$router.push('xie_modify_password')
						

					} else {
						MessageBox('提示', '验证码输入错误');

					}
				})

			},
			next() {
				this.Passwordvalid()
			}
		},
		mounted() {
						this.onloadd()
			this.yanzm()
		},
		filters: {
			numbe: function(phone) {
				let reg = /^(\d{3})(\d{4})(\d{4})$/;
				phone = phone.replace(reg, "$1****$2");
				return phone
			}
		}

	}
</script>
<style lang="less" scoped>
	.header-grop {
		.buttom_box {
			margin: 0 auto;
			margin-top: .6rem;
			width: 90%;
			height: .88rem;
		}
		.img_phone {
			margin-top: 1rem;
			display: flex;
			flex-direction: column;
			/*justify-content:center;
		align-content: center;*/
			text-align: center;
			#AccountNumber {
				margin: 0 auto;
				display: flex;
				/*justify-content: center;*/
				align-items: center;
				span {
					margin-left: .2rem;
					/*padding: .1rem;*/
					background: #F1C50E;
					color: #fff;
					height: .8rem;
					width: 1.6rem;
					line-height: .8rem;
					border-radius: 10px;
				}
				input {
					border-radius: 5px;
					height: .8rem;
					width: .6rem;
					line-height: .8rem;
					outline: none;
					text-align: center;
					font-size: .3rem;
					/*background-color: #DDE4FF;*/
					margin-left: .1rem;
					border: 2px solid #999;
				}
			}
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
			/*input {
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
		}*/
		}
	}
</style>