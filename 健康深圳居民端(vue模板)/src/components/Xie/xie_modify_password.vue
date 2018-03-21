<template>
	<div class="header-grop">
		<mt-header title="忘记密码" style="background: #FFFFFF;font-size: 0.3rem;color: #000000;">
			  <router-link to="/xie_verification" slot="left">
			    <mt-button icon="back"></mt-button>
			  </router-link>
		</mt-header>
		<div class="img_phone">
			<div>
				<img src="../../assets/img/xie_modify.png" >
			</div>
			<span>新密码由6-20数组或英文字母组成</span>
			<div class="inpu">
				<input type="text" placeholder="请输入新密码" v-model="password" ref="pwd">
				<div @click="valp" class="home_delete" v-show="isshow3" >
						<img src="../../assets/img/xie_express.png">
				</div>
				<div @click="valp" class="home_delete" v-show="!isshow3">
						<img  src="../../assets/img/xie_the_dark.png" >
				</div>
			</div>
			<div class="buttom_box">
				<mt-button size="large" @click="succ" style="background:#5EC671;color: #fff;font-size: .32rem;">确定</mt-button>
			</div>
		</div>
	</div>
</template>
<script>
var md5 = require("md5");
import { commonAjax,getValidation}
from '../../api/api';
import {MessageBox }from 'mint-ui';
export default {

    components: {

    },
    data() {
        return {
			password:'',
			isshow3:true
        }

    },
    computed: {

    },
    methods: {
    	succ () {
    		if(/^[\w.]{6,20}$/.test(this.password)){ 
		      	this.Passwordvalid();
		      	
		    }else{
		    	MessageBox("密码由6-20位数字英文字母组成")
		    		}
    	},
    	valp(){
    		if(this.isshow3==true){
    			this.isshow3=false
    			this.$refs.pwd.type = "password"
//  			console.log(this.$refs.type)
    		}else{
    			this.isshow3=true
    			this.$refs.pwd.type = "text"
    		}
    		console.log(this.$refs.type)
    	},
        Passwordvalid() {
        	console.log(sessionStorage.getItem('xie_username'))
                let params = ["hcn.shenzhen","patient",sessionStorage.getItem('xie_username'),md5(this.password)]
                getValidation(JSON.stringify(params), 'hcn.register', 'findPassword').then(res => {
                     if (res.code == 200) {
                     	sessionStorage.setItem("xie_username",this.phones);
                     	MessageBox("密码修改成功")
						this.$router.push('xie_homepage')
                    }
                })

            },
    },
    mounted() {
    },
}
</script>
<style lang="less" scoped>
.header-grop{
	.img_phone{
		margin-top: 1rem;
		display:flex;
		flex-direction:column;
		/*justify-content:center;
		align-content: center;*/
		text-align: center;
		>img{
			width: .4rem;
			height: .4rem;
			position: absolute;
			top: 0;
			right: 0;
		}
		div:first-child{
			/*text-align: center;*/
			img{
			width: 2rem;
			height: 2rem;
			}
		}
		span{
			margin-top: .6rem;
			font-size: .28rem;
			color: #35b46f;
		}
		.inpu{
			margin: 0 auto;
			width: 80%;
			display: flex;
			justify-content: space-around;
			border-bottom: 1px solid #999;
			div{
				img{
					width: .5rem;
					height: .5rem;
				}
			}
			input{
				margin: 0 auto;
				text-align: center;
				margin-top: .4rem;
				font-size: .32rem;
				color: #999;
				border: none;
				outline: none;
				width: 80%;
				padding: 0 0 .4rem 0;
			}
		}
		.buttom_box{
			margin:0 auto;
			margin-top: .6rem;
			width: 80%;
			height: .88rem;
		}
	}
}
</style>
