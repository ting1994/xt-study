<template>
    <div class="app" style="overflow-x:hidden;height:100vh;background-color: #f2f2f2;">
        <div class="header">
	        <mt-header title="卡介苗">
	            <router-link to="/childVaccinationStatus" slot="left">
	                <mt-button icon="back"></mt-button>
	            </router-link>
	        </mt-header>
	    </div>
        <div class="session">
        	<mt-cell title="是否已接种">
			    <label class="mint-switch">
					<input class="mint-switch-input" type="checkbox">
					<span class="mint-switch-core"></span>
					<div class="mint-switch-label"></div>
				</label>
			</mt-cell>
			<mt-cell title="接种日期" is-link value="请选择日期"></mt-cell>
			<div class="vaccine_presentation">
				<div>
					<h3>接种效果</h3>
					<p>在婴儿接种卡疫苗3个月后，即婴儿满3个月后应到指定医疗卫生保健机构进行卡介苗接种后效果的检查。</p>
				</div>
				<div>
					<h3>接种部位</h3>
					<p>在婴儿</p>
				</div>
				<div>
					<h3>接种禁忌</h3>
					<p>在婴儿</p>
				</div>
			</div> 
			


        	

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
import { MessageBox,Toast,Badge,Cell,Switch } from 'mint-ui'
export default {
    data: function() {
        return {
            navName: [{name:"深圳市"},{name:"全部等级"},{name:"全部类型"}],
            navSelectName: [{name1:"全部",name2:"一级"},{name1:"全部",name2:"综合"}],
            hotHospitalList:[],
            filterHotHospitalList:[],
            /*hospitalLevel: [{name:"一级",value:"10"},{name:"一级甲等",value:"11"},{name:"一级乙等",value:"12"},{name:"一级丙等",value:"13"},{name:"二级",value:"20"},{name:"二级甲等",value:"21"},{name:"二级乙等",value:"22"},
            				{name:"二级丙等",value:"23"},{name:"三级",value:"30"},{name:"三级特等",value:"31"},{name:"三级甲等",value:"32"},{name:"三级乙等",value:"33"},{name:"三级丙等",value:"34"}],*/
            hospitalLevelName: {"0":"全部","10":"一级","11":"一级甲等","12":"一级乙等","13":"一级丙等","20":"二级","21":"二级甲等","22":"二级乙等","23":"二级丙等","30":"三级","31":"三级特等","32":"三级甲等","33":"三级乙等","34":"三级丙等"},
            hospitalTypeName: {
            				"0":"全部","01":"综合医院","02":"体检中心","03":"妇幼保健院","04":"妇产(科)医院","05":"儿童医院","06":"肿瘤医院","07":"心血管病医院","08":"胸科医院","09":"口腔医院","10":"眼科医院","11":"耳鼻喉科医院","12":"血液病医院","13":"精神病医院","14":"传染病医院","15":"皮肤病医院","16":"结核病医院","17":"麻风病医院","18":"职业病医院","19":"骨科医院","20":"康复医院","21":"整形美容"
            			  },
            /*flag:0*/
        }
    },
    created() {
        
    },
    methods: {
    	a(obj){return document.getElementById(obj)},
    	clickNav(e) {
    		var index = e.currentTarget.id;
    		if(index==0){
        		return;
        	}
    		var that = this;
        	var selectContent = document.getElementById("selectContent");
        	var selectNavContent = document.getElementById("selectContent").children;
        	var modal = document.getElementById("gray");
        	var flag = e.currentTarget.getAttribute("flag");
        	var selectNav = document.getElementById("nav").children;
        	for(var i=0;i<selectNav.length;i++){
	        	selectNav[i].classList.remove('active');
	        }
        	for(var i=0;i<selectNavContent.length;i++){
        		selectNavContent[i].style.display="none";
        	}
        	if(flag==0){
        		modal.style.display="block";
        		selectContent.style.display="block";
        		selectNavContent[index-1].style.display="block";
        		e.currentTarget.setAttribute("flag",1);
        		e.currentTarget.classList.add('active');
        	}else{
        		selectContent.style.display="none";
        		modal.style.display="none";
        		e.currentTarget.setAttribute("flag",0);
        	}
        	//点击任意位置，隐藏下拉列表selectContent
        	this.stopBubble(e); 
        	document.onclick=function(){
		        that.a("selectContent").style.display='none';
		        that.a("gray").style.display='none';
		        that.a("nav").children[1].setAttribute("flag",0);
		        that.a("nav").children[2].setAttribute("flag",0);
	        	for(var i=0;i<selectNav.length;i++){
		        	selectNav[i].classList.remove('active');
		        }
		　　　　　 document.onclick=null;　
		    }
        	
        },
        selectHosLevel(e,level){
        	this.filterHotHospitalList = [];
        	document.getElementById("selectContent").style.display="none";
        	document.getElementById("gray").style.display="none";
        	document.getElementById("nav").children[1].setAttribute("flag",0);
        	var selectNav = document.getElementById("nav").children;
        	for(var i=0;i<selectNav.length;i++){
	        	selectNav[i].classList.remove('active');
	        }
        	if(level=="0"){
        		this.filterHotHospitalList = this.hotHospitalList;
        		return;
        	}
        	for(var i=0;i<this.hotHospitalList.length;i++){
        		if(this.hotHospitalList[i].level==level){
        			this.filterHotHospitalList.push(this.hotHospitalList[i]);
        		}
        	}
        	if(this.filterHotHospitalList.length==0){
        		Toast({
	                message: '暂无结果',
	                position: 'middle',
	                duration: 1000
	            });
        	}
        },
        selectHosType(e,type){
        	this.filterHotHospitalList = [];
        	document.getElementById("selectContent").style.display="none";
        	document.getElementById("gray").style.display="none";
        	document.getElementById("nav").children[2].setAttribute("flag",0);
        	var selectNav = document.getElementById("nav").children;
        	for(var i=0;i<selectNav.length;i++){
	        	selectNav[i].classList.remove('active');
	        }
        	if(type=="0"){
        		this.filterHotHospitalList = this.hotHospitalList;
        		return;
        	}
        	for(var i=0;i<this.hotHospitalList.length;i++){
        		if(this.hotHospitalList[i].nature==type){
        			this.filterHotHospitalList.push(this.hotHospitalList[i]);
        		}
        	}
        	if(this.filterHotHospitalList.length==0){
        		Toast({
	                message: '暂无结果',
	                position: 'middle',
	                duration: 1000
	            });
        	}
        },
        //阻止冒泡函数
		stopBubble(e){  
		    if(e && e.stopPropagation){
		        e.stopPropagation();  //w3c
		    }else{
		        window.event.cancelBubble=true; //IE
		    }
		},
        getHotHospitalList(){
        	let params = [1,100];
	        /*commonAjax(params, 'hcn.easyDoctor', 'getHotHospitals').then(res => {
	            if (res.code === 200) {
	                this.hotHospitalList = res.body
	                console.log(res.body);
	            }
	        });*/
	        commonAjax(params, 'hcn.easyDoctor', 'getHotHospitals').then(res => {
                if (res.code === 200) {
                    if (res.body.length) {
                        this.hotHospitalList = res.body
                        this.filterHotHospitalList = res.body
                    } else {
                        this.hotHospitalList = []
                        this.filterHotHospitalList = []
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
    	var _this = this;
        this.getHotHospitalList();
        this.a('selectContent').onclick=function(event){
		    //只阻止了向上冒泡，而没有阻止向下捕获，所以点击con的内部对象时，仍然可以执行这个函数
		    _this.stopBubble(event); 
		}
    },
    destroyed() {
    	
    }
}
</script>

<style lang='stylus' scoped>
mainColor = #4eab52
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
    .search{
    	display:block;
    	float:right;
    	width:20px;
    	height:20px;
    	background-image: url('../../assets/img/ssj_search_white.png');
    	background-size: 20px 20px;
    }
}
.session {
    margin-top: 1rem;
    margin-bottom: 1rem;
    color:#666;
} 
.mint-switch-input:checked + .mint-switch-core{
	background-color:#36bf84;
	border-color:#36bf84;
}
.vaccine_presentation{
	background-color:#fff;
	font-size:0.28rem;
	padding:20px 10px;
	margin-top:10px;
	border-top:1px solid rgba(217,217,217,0.5);
}
.vaccine_presentation div{
	margin-bottom:12px;
}
.vaccine_presentation h3{
	font-size:0.3rem;
	color:#333;
	padding:10px 0;
}
.vaccine_presentation div p{
	line-height:26px;
}




</style>
